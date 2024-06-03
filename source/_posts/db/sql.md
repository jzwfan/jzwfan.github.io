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



