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



