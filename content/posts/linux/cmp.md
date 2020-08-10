---
title: "Linux cmp命令"
date: 2020-08-10T23:07:56+08:00
draft: false
categories: ["每日Linux命令"]
tags: ["Linux"]
---

---

### 前言

Linux 中比较两个文件是否一致有好几种方式，前面已经讲过了 cksum 命令来校验两个文件是否一致，今天来讲一下 cmp 命令。

### 命令详解

Linux cmp 命令用于比较两个文件是否有差异。当相互比较的两个文件完全一样时，则该指令不会显示任何信息。若发现有所差异，预设会标示出第一个不同之处的字符和列数编号。若不指定任何文件名称或是所给予的文件名为"-"，则 cmp 指令会从标准输入设备读取数据。

### 命令全拼

cmp = compare

### 语法格式

> cmp [-clsv][-i <字符数目>][--help][第一个文件][第二个文件]

### 参数说明

- -c或--print-chars: 除了标明差异处的十进制字码之外，一并显示该字符所对应字符。
- -i<字符数目>或--ignore-initial=<字符数目>: 指定一个数目。
- -l或--verbose: 标示出所有不一样的地方。
- -s或--quiet或--silent: 不显示错误信息。
- -v或--version: 显示版本信息。
- --help: 在线帮助。

### 举个栗子

1、要确定两个文件是否相同，请输入：

> cmp yeqiongzhou.jpg yeqiongzhou.jpg.bak

上面命令比较 yeqiongzhou.jpg 和 yeqiongzhou.jpg.bak 是否相同。如果文件相同，则不显示消息。

2、如果比较的两个文件不同，则显示第一个不同的位置，例如：

> cmp yeqiongzhou1.jpg yeqiongzhou2.jpg  
> yeqiongzhou1.jpg yeqiongzhou2.jpg differ: char 22, line 1

### Tips

如果显示消息 cmp: EOF on yeqiongzhou1.jpg，则 yeqiongzhou2.jpg 的第一部分与 yeqiongzhou1.jpg 相同，但在 yeqiongzhou2.jpg 中还有其他数据。
