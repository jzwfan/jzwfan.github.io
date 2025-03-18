---
title: conda占用高CPU问题
cover: /img/cover/7.jpg
hide: false
date: 2025-03-11 13:45:24
permalink: python/conda-problem0.html
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

前几天在欧拉系统安装了一个miniconda，用来管理python的各版本，本来系统cpu占用为4%左右，安装后cpu占用一直在20%以上。

---

### 定位问题

用`top`命令发现有一个名为conda的进程一直居高不下，百度发现是当前用户 `～/.bashrc`文件（如果用了omz,文件为`～/.zshrc`）中多了以下一段代码

```shell 

#>>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/root/miniconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
   if [ -f "/root/miniconda3/etc/profile.d/conda.sh" ]; then
        . "/root/miniconda3/etc/profile.d/conda.sh"
   else
       export PATH="/root/miniconda3/bin:$PATH" # 这里根据安装的软件不同而有不同变化
   fi
fi
## unset __conda_setup
# <<< conda initialize <<<

```

### 处理方式

- 1、注释或删除该代码
- 2、在`～/.bashrc`（`~/.zshrc`）文件最后添加

```shell 
# 安装不同软件文件夹名不同
export PATH="/root/miniconda3/bin:$PATH"
```

---

参考地址：https://blog.csdn.net/weixin_43495948/article/details/129459638
