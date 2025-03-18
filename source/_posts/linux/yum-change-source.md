---
title: yum换源
cover: /img/cover/17.jpg
hide: false
date: 2024-07-09 13:56:57
permalink: linux/yum-change-source.html
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

使用yum的官方源进行yum install xxxx 的时候，速度非常慢，只有几kB/s，有时候还不到1kB/s。这就会造成安装包的速度的速度要么特变慢，要么就根本安装不了。

---

### 更新源

#### 备份

```shell
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak
```

#### 下载新的 CentOS-Base.repo 到 /etc/yum.repos.d/

```shell
# Centos6
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
# Centos7
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

注：如果没有安装`wget`，可本地访问网址下载，上传到服务器。

#### 清理并生成新的缓存

```shell
yum clean & yum makecache
```

### 总结

有时候可能阿里源不可用，可替换清华源等。

原地址：https://blog.csdn.net/wudinaniya/article/details/105758739
