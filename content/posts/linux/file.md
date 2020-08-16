---
title: "Linux file命令"
date: 2020-08-16T17:13:14+08:00
draft: false
categories: ["每日Linux命令"]
tags: ["Linux"]
---

---

### 前言

Linux 中“一切皆文件”，任何事物都是以文件的形式存在，在 windows 环境下，我们一般情况下可以通过文件的后缀名来识别文件的种类，但是在 linux 环境下，文件名可以自由更改，这时我们就可以通过 file 命令来获取文件的类型信息。

### 命令详解

Linux file 命令用于辨识文件类型，通过 file 指令，我们得以辨识该文件的类型。

### 语法格式

> file [-bcLvz][-f <名称文件>][-m <魔法数字文件>...][文件或目录...]

### 参数说明

- -b 　列出辨识结果时，不显示文件名称。
- -c 　详细显示指令执行过程，便于排错或分析程序执行的情形。
- -f<名称文件> 　指定名称文件，其内容有一个或多个文件名称时，让file依序辨识这些文件，格式为每列一个文件名称。
- -i 　显示MIME类别。
- -L 　直接显示符号连接所指向的文件的类别。
- -m<魔法数字文件> 　指定魔法数字文件。
- -v 　显示版本信息。
- -z 　尝试去解读压缩文件的内容。
- [文件或目录...]  要确定类型的文件列表，多个文件之间使用空格分开，可以使用shell通配符匹配多个文件。

### 举个栗子

1、显示文件类型：

> file yetalks.mp4  
> yetalks.mp4: ISO Media, MP4 v2 [ISO 14496-14]

2、不显示文件名称：

> file -b yetalks.mp4  
> ISO Media, MP4 v2 [ISO 14496-14]

3、显示MIME类别：

> file -i yetalks.log  
> yetalks.log: text/plain; charset=utf-8

### Tips

Linux 一切皆文件。
