---
title: "Linux nslookup 命令"
date: 2021-01-30T15:13:14+08:00
categories: ["每日Linux命令"]
tags: ["Linux"]
---

---

### 前言

　　我们在工作时经常会查看某个 IP 或域名的 DNS 信息，查看当前 IP 绑定到了哪台机器上，或者当前域名是否解析正常。这里就要用到 nslookup 命令了。在使用 nslookup之前，先确保已经安装了它，nslookup 属于 bind-utils 包下一个命令。

### 命令详解

nslookup 命令主要用来查询域名的 DNS 信息。
nslookup 有两种工作模式：“交互模式” 和 “非交互模式”。在命令行中直接输入 nslookup，无需输入任何参数即进入交互模式。

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
