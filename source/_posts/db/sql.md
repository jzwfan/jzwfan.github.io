---
title: Sql语句
cover: /img/cover/14.jpg
hide: false
date: 2024-06-03 17:33:25
permalink: db/sql.html
tags:
 - Mysql
 - DM
categories:
 - 数据库
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

工作中遇到的SQL查询方法、语法、和优化记录。

----

### SQL 方法和关键字

#### GROUP_COUNT\WM_COUNT

```sql
# mysql group_concat
# separator 用来替换拼接字段， eg: 水果-素菜
select
	group_concat(c.category_name separator '-') category_name,
	cs.store_id
from
	dt_category_store as cs
	inner join
	dt_category as c
	on 
		cs.category_id = c.category_id and cs.category_type = 6
group by cs.store_id
```

```sql
# dm wm_concat 方式
select
	wm_concat(c.category_name) category_name,
	cs.store_id
from
	dt_category_store as cs
	inner join
	dt_category as c
	on 
		cs.category_id = c.category_id and cs.category_type = 6
group by cs.store_id
```

#### LEFT（从**左**开始截取字符串）

用法：left(str, length)，即：left(被截取字符串， 截取长度)

```sql
SELECT LEFT('www.jzwfan.com',8)
```

结果为：www.jzwf

#### RIGHT(从**右**开始截取字符串)

用法：right(str, length)，即：right(被截取字符串， 截取长度)

```SQL
SELECT RIGHT('www.jzwfan.com',6)
```

结果为：an.com

#### SUBSTRING(截取**特定长度**的字符串)

用法：

- substring(str, pos)，即：substring(被截取字符串， 从第几位开始截取)
- substring(str, pos, length)，即：substring(被截取字符串，从第几位开始截取，截取长度)

1.从字符串的第9个字符开始读取直至结束

```sql
SELECT SUBSTRING('www.jzwfan.com', 9)
```

结果为：an.com

2.从字符串的第5个字符开始，只取3个字符

```sql
SELECT SUBSTRING('www.jzwfan.com', 5, 3)
```

结果为：jzw

3.从字符串的倒数第6个字符开始读取直至结束

```sql
SELECT SUBSTRING('www.jzwfan.com', -6)
```

结果为：an.com

4.从字符串的倒数第6个字符开始读取，只取2个字符

```sql
SELECT SUBSTRING('www.jzwfan.com', -6, 2)
```

结果为：an

#### SUBSTRING_INDEX(按**关键字**进行读取)

用法：substring_index(str, delim, count)，即：substring_index(被截取字符串，关键字，关键字出现的次数)

1.截取第二个“.”之**前**的所有字符

```sql
SELECT SUBSTRING_INDEX('www.jzwfan.com', '.', 2);
```

结果为：www.jzwfan

2.截取倒数第二个“.”之**后**的所有字符

```sql
SELECT SUBSTRING_INDEX('www.jzwfan.com', '.', -2);
```

结果为：jzwfan.com

3.如果关键字不存在，则返回整个字符串

```sql
SELECT SUBSTRING_INDEX('www.yuanrengu.com', 'sprite', 1);
```

结果为：www.jzwfan.com

以上，源地址：https://www.cnblogs.com/heyonggang/p/8117754.html

#### FROM_UNXITIME(时间戳格式化)

```sql
# FROM_UNXITIME(unix_timestamp, format)
SELECT FROM_UNXITIME(1459338786, '%Y-%m-%d %H:%i:%s');
```

format格式说明：

%M 月名字(January～December)
%W 星期名字(Sunday～Saturday)
%D 有英语前缀的月份的日期(1st, 2nd, 3rd, 等等。）
%Y 年, 数字, 4 位
%y 年, 数字, 2 位
%a 缩写的星期名字(Sun～Sat)
%d 月份中的天数, 数字(00～31)
%e 月份中的天数, 数字(0～31)
%m 月, 数字(01～12)
%c 月, 数字(1～12)
%b 缩写的月份名字(Jan～Dec)
%j 一年中的天数(001～366)
%H 小时(00～23)
%k 小时(0～23)
%h 小时(01～12)
%I 小时(01～12)
%l 小时(1～12)
%i 分钟, 数字(00～59)
%r 时间,12 小时(hh:mm:ss [AP]M)
%T 时间,24 小时(hh:mm:ss)
%S 秒(00～59)
%s 秒(00～59)
%p AM或PM
%w 一个星期中的天数(0=Sunday ～6=Saturday ）
%U 星期(0～52), 这里星期天是星期的第一天
%u 星期(0～52), 这里星期一是星期的第一天
%% 一个文字%

原地址：https://blog.csdn.net/fdipzone/article/details/51018930

#### DROP（删除表｜通用）

```sql
# Mysql
DROP TABLE 表名;
# DM
DROP TABLE 空间名.表名;
```

#### TRUNCATE（清空表数据｜通用）

```sql
# Mysql
TRUNCATE TABLE 表名;
# DM
TRUNCATE TABLE 空间名.表名;
```



### SQL一些常用命令

#### DM设置表主键是否自动递增

```sql
# OFF 开启， ON 关闭
SET IDENTITY_INSERT 空间名.表名 ON;
```

### DM添加索引例子

```sql
CREATE OR REPLACE  INDEX "索引名" ON "空间名"."表名"("列名1" ASC,"列名2" ASC,"列名3" ASC...) STORAGE(ON "MAIN", CLUSTERBTR);
```

#### DM创建表语句模版

```sql
CREATE TABLE "空间名"."表名"
(
"ID" BIGINT IDENTITY(1, 1) NOT NULL,
"NEIBH_ID" BIGINT,
"CATEGORY_ID" BIGINT,
"CATEGORY_TYPE" VARCHAR(2),
"INSPECTOR_IDS" VARCHAR(255) DEFAULT '',
"INSPECTOR_NAMES" VARCHAR(255) DEFAULT '',
"TENANT_ID" INT,
"DELETED" BIT DEFAULT 0,
"CREATOR" INT,
"CREATE_TIME" TIMESTAMP(0),
"UPDATER" INT,
"UPDATE_TIME" TIMESTAMP(0),
NOT CLUSTER PRIMARY KEY("ID")) STORAGE(ON "MAIN", CLUSTERBTR) ;
```



