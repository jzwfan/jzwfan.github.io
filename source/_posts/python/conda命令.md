---
title: conda命令
cover: /img/cover/3.jpg
hide: false
date: 2025-03-11 13:48:27
permalink: python/conda-command.html
tags:
 - python
 - conda
categories:
 - Python
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

记一下conda在Linux系统环境下的安装和应用。

---

### 安装

conda共存在anaconda、miniconda、miniforge、conda等多个不同的工具，这里不过多讨论它们的差别，只讲一下安装miniconda的过程

#### 下载可执行安装文件

文件地址：`https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh`

注：anaconda下载地址为

`https://repo.anaconda.com/archive/Anaconda3-5.3.0-Linux-x86_64.sh`

![](https://images.jzwfan.com/image/2025/03/11/143359-0.png)

#### 执行安装命令

根据提示一直输入`yes`即可

![](https://images.jzwfan.com/image/2025/03/11/144437-0.png)

#### 验证是否安装完成

运行`conda --version`打印出版本号证明已安装成功

![image-20250311145758305](https://images.jzwfan.com/image/2025/03/11/145803-0.png)

如果提示不存在的命令，在`.bashrc`文件中加入以下命令再刷新命令即可，具体命令如下：

```shell
cd ~ # 切换到家目录
# 在.bashrc最后一行加入 export PATH="/root/miniconda3/bin:$PATH" 代码
echo 'export PATH="/root/miniconda3/bin:$PATH"' > .bashrc 
# 更新环境变量
source .bashrc 
```

### 应用

#### 创建环境

创建python版本为3.6的环境，取名p36

```shell
conda create -n p36 python=3.6
```

#### 激活\切换环境

```shell
conda activate p36
```

#### 退出环境

```shell
conda deactivate
```

#### 删除环境

```shell
conda remove -n p36 --all
```

#### 查看已有环境

```shell
conda info --env
```

#### 在环境内安装包

已pymsql包为例

```shell
conda activate p36 # 切换到指定环境
conda install pymysql # 安装pymsql包
```

注：如果conda包安装不成功，可用pip来安装

### 后记

anaconda、miniconda、miniforge、conda等多个不同的工具区别参考以下文章：

https://zhuanlan.zhihu.com/p/518926990

安装参考以下文章：

https://blog.csdn.net/wyf2017/article/details/118676765

