---
title: git项目同步上游项目到本项目
cover: /img/cover/9.jpg
hide: false
date: 2025-03-18 17:12:45
permalink: git/git-fork-sync.html
tags:
  - git
  - fork
categories:
  - Git
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

今天工作是遇到部分功能更新要在上游和本地项目中同步更新，不想两个项目都要同步复制代码，于是想到了git fork的子项目可以拉取上游项目的理，便做一下相关记录

---

### 查看项目绑定的远程仓库地址

用以下命令查看当前项目绑定的远程仓库

```shell
git remote -v
```

输出：

```shell
origin	https://github.com/gyx/java-dgjy-build-admin.git (fetch)
origin	https://github.com/gyx/java-dgjy-build-admin.git (push)
```

### 添加新的远程仓库地址

用以下明令添加上游项目的远程仓库的地址：

```shell
# 添加新仓库 upstream(上游) 可以自定义
git remote add upstream https://github.com/gyx/java-dgjy-build.git
# 获取远程仓库地址分支信息
git fetch upstream
```

注：两个仓库有相同的分支名的时候，最好不要直接checkout上游分支，可能和本地分支冲突。

再用上一步命令查看已绑定的远程仓库的地址输出如下：

```shell
origin	https://github.com/gyx/java-dgjy-build-admin.git (fetch)
origin	https://github.com/gyx/java-dgjy-build-admin.git (push)
upstream	https://github.com/gyx/java-dgjy-build.git (fetch)
upstream	https://github.com/gyx/java-dgjy-build.git (push)
```

### 后记

剩下的操作就都可以直接用idea等git管理软件来完成了。
