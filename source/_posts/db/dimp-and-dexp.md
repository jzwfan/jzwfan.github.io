---
title: 达梦数据导入导出
cover: /img/cover/12.jpg
hide: false
date: 2024-07-01 17:12:14
permalink: db/dimp-and-dexp.html
tags:
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

达梦数据库导出导入工具使用说明。备注，此备份还原方案是逻辑操作，在少量数据的情况下，性能足够，一旦数据量过大，则备份时间极长。

### 同步方式

达梦数据库支持4种数据同步方式，这些方式可以根据特定的场景去使用。

- FULL（全库）
- OWNER（用户）
- SCHEMAS（模式）
- TABLES（表）

### 参数说明

<table class="data-table" data-transient-attributes="class"
    style="width: 100%; outline: none; border-collapse: collapse;" data-width="576px">
    <colgroup>
        <col span="1" width="144">
        <col span="1" width="144">
        <col span="1" width="144">
        <col span="1" width="144">
    </colgroup>
    <tbody>
        <tr style="height: 30px;">
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>参数<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>dexp说明<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>dimp说明<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection" class="table-last-row"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>备注<br></p>
            </td>
        </tr>
        <tr style="height: 30px;">
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>USERID<br></p>
            </td>
            <td colspan="2" data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>USERID在作为导出和导入时，都是指定一个链接串。格式为：用户名/密码@库名:端口号#证书路径<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection" class="table-last-row"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
            </td>
        </tr>
        <tr style="height: 30px;">
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>FILE<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>file作为导出参数时，指定导出的文件名。可选参数，默认值为dexp.dmp<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>fiel作为导入参数时，指定导入使用的文件名，也就是dexp导出的文件。作为导入时，它是必选参数。<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection" class="table-last-row"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
            </td>
        </tr>
        <tr style="height: 30px;">
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>DIRECTORY<br></p>
            </td>
            <td colspan="2" data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>directory参数指定导出和导入的目录，简单点说就是指定dmp(转储文件)的位置。<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection" class="table-last-row"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
            </td>
        </tr>
        <tr style="height: 30px;">
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>FULL<br></p>
            </td>
            <td colspan="2" data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>full参数指定导出和导入基于整个数据库，也就是导出整个数据库或导入整个数据库。<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection" class="table-last-row"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>四种方式之一，不建议使用。<br></p>
            </td>
        </tr>
        <tr style="height: 30px;">
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>OWNER<br></p>
            </td>
            <td colspan="2" data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>owner参数指定导出和导入基于用户，也就是导出或导入用户中的所有对象，多个用户使用英文逗号分割。<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection" class="table-last-row"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>四种方式之一，根据需要使用，用户与模式基本一致。<br></p>
            </td>
        </tr>
        <tr style="height: 30px;">
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>SCHEMAS<br></p>
            </td>
            <td colspan="2" data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>schemas参数指定导出和导入基于模式，也就是导出或导入模式下的所有对象，多个模式使用英文逗号分割<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection" class="table-last-row"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>四种方式之一，根据需要使用，模式与用户基本一致。<br></p>
            </td>
        </tr>
        <tr style="height: 30px;">
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>TABLES<br></p>
            </td>
            <td colspan="2" data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>tables参数指定导出和导入基于表，也就是导出或导入表的结构和数据，多个表使用英文逗号分割。<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection" class="table-last-row"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>四种方式之一，根据需要使用<br></p>
            </td>
        </tr>
        <tr style="height: 30px;">
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>PARALLEL<br></p>
            </td>
            <td colspan="2" data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>parallel参数指定导出和导入过程中使用的线程数。<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection" class="table-last-row"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
            </td>
        </tr>
        <tr style="height: 30px;">
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>COMPRESS<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>compress参数指定导出的数据是否压缩，默认值N(不压缩)，可选值Y|N。<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>无<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection" class="table-last-row"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
            </td>
        </tr>
        <tr style="height: 30px;">
            <td data-transient-attributes="table-cell-selection" class="table-last-column"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>LOG<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection" class="table-last-column"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>log作为导出参数时，指定导出日志的文件名。可选参数，默认值为dexp.log。<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection" class="table-last-column"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
                <p>log作为导入参数时，指定导入日志的文件名。可选参数，默认值为dimp.log。<br></p>
            </td>
            <td data-transient-attributes="table-cell-selection" class="table-last-column table-last-row"
                style="min-width: auto; overflow-wrap: break-word; margin: 4px 8px; border: 1px solid rgb(217, 217, 217); padding: 4px 8px; cursor: default; vertical-align: top;">
            </td>
        </tr>
    </tbody>
</table>

### 使用案例

这里只记录了备份还原模式的用法，其他用法可看原文档

```sql
# 备份
./dexp SYSDBA/SYSDBA001@127.0.0.1:5236 FILE=SZSQ.dmp LOG=SZSQ.log DIRECTORY=/data SCHEMAS=SZSQ
# 还原，还原之前要删除相应表数据
./dimp SYSDBA/SYSDBA001@127.0.0.1:5236 FILE=SZSQ.dmp LOG=SZSQ.log DIRECTORY=/data SCHEMAS=SZSQ

```

原地址：https://blog.51cto.com/bxbdba/7175810