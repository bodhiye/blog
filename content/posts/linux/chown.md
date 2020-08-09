---
title: "Linux chown命令"
date: 2020-08-09T22:44:22+08:00
draft: false
categories: ["每日Linux命令"]
tags: ["Linux"]
---

---

### 前言

Linux/Unix 是多人多工操作系统，所有的文件皆有拥有者。利用 chown 将指定文件的拥有者改为指定的用户或组，用户可以是用户名或者用户ID；组可以是组名或者组ID；文件是以空格分开的要改变权限的文件列表，支持通配符。

### 命令详解

chown 命令，主要用于修改文件（或目录）的所有者，除此之外，这个命令也可以修改文件（或目录）的所属组。

### 命令全拼

chown = change owner

### 语法格式

> chown [-cfhvR] [--help] [--version] user[:group] file...

### 参数说明

- user : 新的文件拥有者的使用者 ID
- group : 新的文件拥有者的使用者组(group)
- -c : 显示更改的部分的信息
- -f : 忽略错误信息
- -h :修复符号链接
- -v : 显示详细的处理信息
- -R : 处理指定目录以及其子目录下的所有文件
- --help : 显示辅助说明
- --version : 显示版本

### 举个栗子

1、将文件 yeqiongzhou.jpg 的拥有者设为 bodhiye，群体的使用者 xiaoye:

> chown bodhiye:xiaoye yeqiongzhou.jpg

2、将目前目录下的所有文件与子目录的拥有者皆设为 bodhiye，群体的使用者 xiaoye:

> chown -R bodhiye:xiaoye *

3、chown 命令也支持单纯的修改文件或目录的所属组：

> chown :xiaoye yeqiongzhou.jpg

就表示修改 yeqiongzhou.jpg 文件的所属组为 xiaoye，但修改所属组通常使用 chgrp 命令，因此只修改文件所属组时并不推荐大家使用 chown 命令。

### Tips

一般来说，这个指令只有是由系统管理者(root)所使用，一般使用者没有权限可以改变别人的文件拥有者，也没有权限把自己的文件拥有者改设为别人。只有系统管理者(root)才有这样的权限。
