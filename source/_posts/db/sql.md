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



