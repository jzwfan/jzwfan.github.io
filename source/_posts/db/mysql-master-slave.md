---
title: mysql主从设置
cover: /img/cover/15.jpg
hide: false
date: 2024-07-12 17:19:19
permalink: db/mysql-master-slave.html
tags:
categories:
 - Mysql
keywords:
description:
top_img:
comments:
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
abcjs:
---

### 前言

公司服务器迁徙之后，因为数据库数据量太大，用备份的数据恢复到从库的方式过于耗费时间，再加上数据库本就是docker方式启动的，以前只是按照文档一步步搭建主从数据库，今天有时间就好好研究一下原理，记录一下偷懒时遇到的问题。

### 搭建过程

注：本方案是为了应对公司项目做的处理，所以处理方式有些偏向与容器化部署项目的记录方案，比如公司本有一台运行中的docker mysql数据库，扩容另台或多台从数据库时可用该方案。

#### 备份主库挂载文件夹到从库服务器

备份文件夹时最好先停止docker容器，或锁表：

```sql
flush tables with read lock
```

备份完成，再恢复数据写入：

```sql
unlock tables
```

#### 如有设置过主从，删除相关表数据，重置设置

截断`mysql`数据库下的`slave_master_info`和`slave_relay_log_info`两个表

![image-20240712174756001](https://images.jzwfan.com/image/2024/07/12/174758-0.png)

删除挂载出来的文件夹下的所有`relay log` 文件（注：挂载出来的为`/var/lib/mysql`文件夹）

![image-20240712175814774](https://images.jzwfan.com/image/2024/07/12/175817-0.png)

数据库中运行以下命令重置状态

```sql
reset slave;
```

#### 更新备库的server-uuid

主库和从库的server-uuid不能相同，这里是直接拷贝文件，所以要手动改配置。用以下命令获取UUID

```sql
SELECT UUID();
```

![image-20240715100907937](https://images.jzwfan.com/image/2024/07/15/100910-0.png)

更新`auto.cnf`文件中的`server-uuid`设置（注：挂载出来的为`/var/lib/mysql`文件夹）

![image-20240715101804553](https://images.jzwfan.com/image/2024/07/15/101813-0.png)

#### my.cnf文件配置

```cnf
[client]
port = 3306
socket = /tmp/mysql.sock

[mysqld]
basedir = /usr/local/mysql
port = 3306
socket = /tmp/mysql.sock
datadir = /usr/local/mysql/data
pid-file = /usr/local/mysql/data/mysql.pid
log-error = /usr/local/mysql/data/mysql.err

server-id = 1 																													#另一个改成2
auto_increment_offset = 1																								#奇数ID，另一个改成偶数ID
auto_increment_increment = 2                                            #ID生成步长改成2

log-bin = mysql-bin                                                     #打开二进制功能,MASTER主服务器必须打开此项
binlog-format=ROW
# binlog-row-p_w_picpath=minimal
#将复制事件写入binlog,一台服务器既做主库又做从库此选项必须要开启
log-slave-updates=true																									
gtid-mode=on
enforce-gtid-consistency=true
master-info-repository=TABLE
relay-log-info-repository=TABLE
sync-master-info=1
slave-parallel-workers=0
sync_binlog=0
binlog-checksum=CRC32
master-verify-checksum=1
slave-sql-verify-checksum=1
binlog-rows-query-log_events=1
#expire_logs_days=5
max_binlog_size=1024M                                                   #binlog单文件最大值

replicate-ignore-db = mysql                                             #忽略不同步主从的数据库
replicate-ignore-db = information_schema
replicate-ignore-db = performance_schema
replicate-ignore-db = test
replicate-ignore-db = zabbix

max_connections = 3000
max_connect_errors = 30

skip-character-set-client-handshake                                     #忽略应用程序想要设置的其他字符集
init-connect='SET NAMES utf8'                                           #连接时执行的SQL
character-set-server=utf8                                               #服务端默认字符集
wait_timeout=1800                                                       #请求的最大连接时间
interactive_timeout=1800                                                #和上一参数同时修改才会生效
sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES                     #sql模式
max_allowed_packet = 10M
bulk_insert_buffer_size = 8M
query_cache_type = 1
query_cache_size = 128M
query_cache_limit = 4M
key_buffer_size = 256M
read_buffer_size = 16K

skip-name-resolve
slow_query_log=1
long_query_time = 6
slow_query_log_file=slow-query.log
innodb_flush_log_at_trx_commit = 2
innodb_log_buffer_size = 16M

[mysql]
no-auto-rehash

[myisamchk]
key_buffer_size = 20M
sort_buffer_size = 20M
read_buffer = 2M
write_buffer = 2M

[mysqlhotcopy]
interactive-timeout

[mysqldump]
quick
max_allowed_packet = 16M

[mysqld_safe]
```

#### 添加主从同步账户

master0

```sql
grant replication slave on *.* to 'repl'@'master1-ip' identified by '123456';
flush privileges;
```

master1

```sql
grant replication slave on *.* to 'repl'@'master0-ip' identified by '123456';
flush privileges;
```

注：为了数据安全，用户最好指定IP而非`%`

#### 查看两个数据库的master状态

命令如下：

```sql
show master status;
```

返回如下图所示，记住被框住的两个数据，后面有用：

![image-20240715104551372](https://images.jzwfan.com/image/2024/07/15/104554-0.png)

#### 配置同步信息

Master0命令如下：

```sql
change master to
master_host='master1-ip', # 指定IP
master_port=3306, # 指定端口
master_user='repl', # 指定用户名
master_password='123456', # 指定用户名字
master_log_file='mysql-master1-bin.000001', # 指定上一步中返回文件名
master_log_pos=582; # 指定上一步中返回的步数
```

然后启动主从:

```sql
start slave;
```

查看状态：

```sql
show slave status\G # 注：这里没有分号
```

显示如下图：

![image-20240715110013349](https://images.jzwfan.com/image/2024/07/15/110015-0.png)

然后在master1上重复此步骤。

### 总结

- 如果以前做过主从，要清理主从配置
- 如果不是导入的，而是和我一样直接复制docker挂载的文件夹时要改server-uuid

参考地址：

https://www.cnblogs.com/ygqygq2/p/6045279.html

https://www.jianshu.com/p/805dc6576b79



