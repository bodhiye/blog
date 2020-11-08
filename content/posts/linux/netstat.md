---
title: "Linux netstat 命令"
date: 2020-11-08T19:55:08+08:00
draft: false
categories: ["每日Linux命令"]
tags: ["Linux"]
---

---

### 前言

在平时的开发过程中，我们会经常遇到查看某个端口占用的情况，一般我们会用到 lsof 和 netstat 这两个命令来查看端口占用信息。

上一篇文章讲解了 lsof 命令，本文就来讲解另一个常用来查看端口信息的 netstat 命令。

### 命令详解

Linux netstat 命令用于显示网络状态，利用 netstat 命令可让你得知整个 Linux 系统的网络情况

### 命令全拼

netstat = network statistic

### 语法格式

> netstat [-acCeFghilMnNoprstuvVwx][-A<网络类型>][--ip]

### 参数说明

- -a或--all 显示所有连线中的Socket。
- -A<网络类型>或--<网络类型> 列出该网络类型连线中的相关地址。
- -c或--continuous 持续列出网络状态。
- -C或--cache 显示路由器配置的快取信息。
- -e或--extend 显示网络其他相关信息。
- -F或--fib 显示FIB。
- -g或--groups 显示多重广播功能群组组员名单。
- -h或--help 在线帮助。
- -i或--interfaces 显示网络界面信息表单。
- -l或--listening 显示监控中的服务器的Socket。
- -M或--masquerade 显示伪装的网络连线。
- -n或--numeric 直接使用IP地址，而不通过域名服务器。
- -N或--netlink或--symbolic 显示网络硬件外围设备的符号连接名称。
- -o或--timers 显示计时器。
- -p或--programs 显示正在使用Socket的程序识别码和程序名称。
- -r或--route 显示Routing Table。
- -s或--statistics 显示网络工作信息统计表。
- -t或--tcp 显示TCP传输协议的连线状况。
- -u或--udp 显示UDP传输协议的连线状况。
- -v或--verbose 显示指令执行过程。
- -V或--version 显示版本信息。
- -w或--raw 显示RAW传输协议的连线状况。
- -x或--unix 此参数的效果和指定"-A unix"参数相同。
- --ip或--inet 此参数的效果和指定"-A inet"参数相同。

### 活学活用

netstat -tunlp 用于显示 tcp，udp 的端口和进程等相关情况。

netstat 查看端口占用语法格式：
> netstat -tunlp | grep 端口号

- -t (tcp) 仅显示tcp相关选项
- -u (udp) 仅显示udp相关选项
- -n 拒绝显示别名，能显示数字的全部转化为数字
- -l 仅列出在Listen(监听)的服务状态
- -p 显示建立相关链接的程序名

### 举个栗子

1、 查看 8000 端口的情况，使用以下命令：

> netstat -tunlp | grep 8000

2、 在 Mac 系统下该命令使用参数有点变化，即`-f`需要加上地址族，`-p`需要加上协议 TCP 或者 UDP 等：

> netstat -anvp | grep 8000
