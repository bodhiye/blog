---
title: "Linux nohup命令"
date: 2021-01-30T15:13:14+08:00
categories: ["每日Linux命令"]
tags: ["Linux"]
---

---

### 前言

我们平时在远程服务器或者跳板机上执行命令时，如果由于长时间未操作导致服务端未响应，触发了防火墙的闲置超时断开的缺省机制，会导致之前执行的命令中断。

### 命令详解

nslookup命令主要用来查询域名的DNS信息。
nslookup有两种工作模式：“交互模式” 和 “非交互模式”。在命令行中直接输入 nslookup，无需输入任何参数即进入交互模式。

### 命令全拼

nslookup = query Internet name server interactively

### 语法格式

> nslookup [参数] [域名]

### 参数说明

- set type=a：设置查询域名A记录。
- set type=mx：设置查询域名邮件交换记录。

### 举个栗子

1、在非交互模式下查询域名基本信息：

> nslookup yeqiongzhou.com

``` bash
Server:         100.100.36.1
Address:        100.100.36.1#53

Non-authoritative answer:
Name:   yeqiongzhou.com
Address: 185.199.108.153
```

2、进入交互模式下查询域名信息：

``` bash
# nslookup
> set type=mx
> yeqiongzhou.com
Server:         100.100.36.1
Address:        100.100.36.1#53

Non-authoritative answer:
yeqiongzhou.com mail exchanger = 10 mxbiz2.qq.com.
yeqiongzhou.com mail exchanger = 5 mxbiz1.qq.com.

Authoritative answers can be found from:
> exit
```
