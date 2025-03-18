---

title: Mybatis下Mapper文件例子
cover: /img/cover/5.jpg
hide: false
date: 2024-06-03 11:39:03
permalink: db/mybatis-mapper.html
tags: 
 - mysql
 - mybatis
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

记一下Mybatis的常用写法，其中也有一些mybatis-plus的写法文档。

----

### choose 用法

```xml
<choose>
    <when test="reqVo.inspectionType == 3">
        SQL1...
    </when>
    <when test="reqVo.inspectionType == 4">
        SQL2...
    </when>
    <otherwise>
        SQL3...
    </otherwise>
</choose>
```

### foreach 用法

```xml
<foreach collection="categoryIds" open="(" separator="," close=")" item="categoryId">
    #{categoryId}
</foreach>
```

