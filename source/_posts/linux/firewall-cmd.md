---
title: 防火墙设置
cover: /img/cover/2.jpg
hide: false
date: 2024-06-28 01:16:57
permalink: linux/firewall-cmd.html
tags:
  - Linux
  - 防火墙
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

记录一下Linux下的firewall-cmd命令的用法，以后慢慢更新，慢慢完善。

---

### 正文

#### 查看防火墙状态

```shell
#查看防火墙状态
systemctl status firewalld
#开启防火墙
systemctl start firewalld
#开机启动
systemctl enable firewalld
```

#### 端口访问设置

查看已开放的端口、IP规则

```shell
#查询打开的端口
firewall-cmd --zone=public --list-ports
```

开放新端口，默认情况下所有端口都是关闭状态

```shell
#开放端口9001/tcp (tcp、udp等)
firewall-cmd --zone=public --add-port=9001/tcp --add-port=9001/udp --permanent
#批量开放9002～9005的tcp端口
firewall-cmd --zone=public --add-port=9002-9005/tcp --permanent
#重新载入防火墙设置，使设置生效
firewall-cmd --reload
```

关闭已开放的端口

```shell
#关闭端口9001/tcp (tcp、udp等)
firewall-cmd --zone=public --remove-port=9001/tcp --add-port=9001/udp --permanent
#批量关闭9002～9005的tcp端口
firewall-cmd --zone=public --remove-port=9002-9005/tcp --permanent
#重新载入防火墙设置，使设置生效
firewall-cmd --reload
```

#### IP访问设置

查看已设置的规则

```shell
#查看已设置的规则
firewall-cmd --zone=public --list-rich-rules
```

开放或限制ip（设置规则）

```shell
#开放IPV4地址为：192.168.0.0 指定端口：9001/tcp
firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="192.168.0.0" port protocol="tcp" port="9001" accept"
#开放IPV4地址为：192.168.0.1，不指定端口，代表可以访问所有端口（是否可以访问未开放端口待验证）
firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="192.168.0.1" accept"
#限制IPV4地址为：192.168.1.0
firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="192.168.1.0" reject"
#重新载入防火墙设置，使设置生效
firewall-cmd --reload
```

删除已设置的规则

```shell
#删除开放IPV4地址为：192.168.0.0 指定端口：9001/tcp
firewall-cmd --permanent --remove-rich-rule="rule family="ipv4" source address="192.168.0.0" port protocol="tcp" port="9001" accept"
#删除开放IPV4地址为：192.168.0.1，不指定端口，代表可以访问所有端口（是否可以访问未开放端口待验证）
firewall-cmd --permanent --remove-rich-rule="rule family="ipv4" source address="192.168.0.1" accept"
#删除限制IPV4地址为：192.168.1.0
firewall-cmd --permanent --remove-rich-rule="rule family="ipv4" source address="192.168.1.0" reject"
#重新载入防火墙设置，使设置生效
firewall-cmd --reload
```

#### 如设置未生效，可尝试直接编辑规则文件，删掉原来的设置规则，重新载入一下防火墙即可

```shell
vi /etc/firewalld/zones/public.xml
```

###参考地址

https://blog.csdn.net/haoqi9999/article/details/125988881
