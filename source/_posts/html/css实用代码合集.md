---
title: css实用代码合集
cover: /img/cover/13.jpg
hide: false
date: 2024-06-06 16:09:43
permalink: html/practical-css.html
tags:
 - 前端
 - css
categories:
 - 前端
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
记录一些在工作和写博客中遇到的一些CSS代码场景,可能这些用的不多，以后也很敢再遇到新的逻辑代码,但总要养成遇到就要记录的习惯。

### img图片保持比例且居中显示

 外部容器设置 固定宽度高度，设置line-height与height相等（垂直居中），设置text-align是center(水平居中)，内部img设置style（max-height:100%;max-width:100%;vertical-align: middle; [margin](https://so.csdn.net/so/search?q=margin&spm=1001.2101.3001.7020): 0 auto;）。

```html
<div style="width: 398px;height: 298px;line-height: 298px;text-align: center;border:1px solid #E09972">
    <img src="test.jpg" style="max-width:100%;max-height:100%;vertical-align: middle; margin: 0 auto;" alt="">
</div>
```

源地址：https://blog.csdn.net/shijie_nihao/article/details/106348591
