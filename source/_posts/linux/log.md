---
title: 系统操作日志相关
cover: /img/cover/1.jpg
hide: false
date: 2024-09-18 11:02:27
permalink: linux/log.html
tags:
  - linux
categories:
  - Linux
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

linux系统的一些日志系统整理。

---

### 查看用户操作日志

```shell
last		#查看最近登录的账户的信息
lastlog		#查看所有账户的最近一次登录信息
```

### 查看用户的操作记录 ： 到用户家目录下查看.bash_history文件

```shell
 cat /home/{username}/.bash_history
```

### 设置操作记录时间格式

```shell
echo 'export HISTTIMEFORMAT="%Y-%m-%d %H:%M:%S "' >> /etc/bash.bashrc 
echo 'export HISTSIZE=-1' >> /etc/bash.bashrc # -1为保存所有
echo 'HISTTIMEFORMAT="%F %T "' >> /etc/profile
source /etc/profile
```



