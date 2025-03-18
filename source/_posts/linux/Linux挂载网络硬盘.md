---
title: Linux挂载网络硬盘
cover: /img/cover/11.jpg
hide: false
date: 2025-03-04 11:37:28
permalink: linux/network-hard-disk.html
tags:
 - linux
 - 网络硬盘
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

Linux开机自动挂载smb网络硬盘

---

### 安装`cifs-utils`插件

#### Redhat系

```shell
# yum 安装
yum install cifs-utils -y
# rpm包安装
# 下载一个cifs-utils的rpm包
rpm -ivh --nodeps cifs-utils.rpm
```

#### Debian系

```shell
# apt 安装
apt install cifs-utils
```

### 挂载

#### 创建用户名密码配置文件

在`/etc`下创建`samba.config`文件，文件内容如下：

```ini
# 你自己nas网盘的用户名和密码
username=用户名
password=密码
```

注：文件名和文件地址不一定要和我的一样，只要下面挂载命令里统一即可

#### 挂载网盘

```shell
# 创建挂载文件夹
mkdir /samba_share
# 在/etc/fstab文件加入下一行代码
# 0.0.0.0 替换成自己的IP
# /nas 替换成自己的网盘共享文件夹地址
# /samba_share 和本地文件夹地址相同
# /etc/samba.config 用户名密码的配置文件地址
//0.0.0.0/nas /samba_share cifs rw,credentials=/etc/samba.config,gid=0,uid=0,rw,iocharset=utf8,file_mode=0777,dir_mode=0777 0 0
```

注：该方式挂载后，系统启动后就能自动挂载，但如此配置不好，可能导致系统启动不了，需用引导系统进入系统才能修改该文件，如果临时用可以用mount 命令挂载，命令如下：

```shell
mount.cifs  //10.10.10.1/nas  /home/nas/  -o username=gz,domain=nas,password=123456,sec=ntlmssp,iocharset=utf8
# 或者
mount -t cifs -o  username=gz,domain=nas,password=123456,sec=ntlmssp,iocharset=utf8   //10.10.10.1/nas  /home/nas/ 
# 如果挂载不上，无反应，就在参数上添加vers=2.0
# 命令参数解析：
mount                         #挂载命令
-t                            #挂载文件系统的类型，通常不必指定。mount会自动选择正确的类型(nas有两种格式：nfs、cifs)
-o iocharset=utf8             [options 主要用来描述设备或档案的挂接方式，\ 参数iocharset表示指定访问文件系统所用字符集。\ 路径中如有中文则添加此项，支持中文路径]
sername=gz                    [nas用户名]
Domain=nas                    [域名]
password=123456               [nas密码]     
//10.10.10.1/nas              [nas路径]
/home/nas/                    [挂载路径]
sec=ntlmssp                   [NTLMSSP (NT LAN Manager Security Support Provider)，是微软提供的安全支持接口协议]
```

### 后记

mount命令挂载参考以下文章，该方式本人没尝试过

https://blog.csdn.net/weixin_39724395/article/details/123429188 

