---
title: "Linux nohup命令"
date: 2020-08-03T23:03:22+08:00
draft: false
categories: ["每日Linux命令"]
tags: ["Linux"]
---

---

### 前言

我们平时在远程服务器或者跳板机上执行命令时，如果由于长时间未操作导致服务端未响应，触发了防火墙的闲置超时断开的缺省机制，会导致之前执行的命令中断。

### 命令详解

nohup 英文全称 no hang up（不挂起），用于在系统后台不挂断地运行命令，退出终端不会影响程序的运行。

nohup命令，在默认情况下（非重定向时），会输出一个名叫 nohup.out 的文件到当前目录下，如果当前目录文件不可写，则输出重定向到 $HOME/nohup.out 文件中。

### 命令全拼

cksum = no hang up

### 语法格式

> nohup Command [ Arg … ] [　& ]

### 参数说明

- Command：要执行的命令。
- Arg：一些参数，可以指定输出文件。
- &：让命令在后台执行，终端退出后命令仍旧执行。

### 举个栗子

1. 以下命令在后台执行 root 目录下的 yeqiongzhou.sh 脚本：

> nohup /root/yeqiongzhou.sh &

以上命令执行后，在终端如果看到以下输出说明运行成功：

> nohup: ignoring input and appending output to 'nohup.out'

这时我们打开 root 目录 可以看到生存了 nohup.out 文件。
如果要停止运行，你需要使用以下命令查找到 nohup 运行脚本到 PID，然后使用 kill 命令来删除。

> ps -aux | grep "yeqiongzhou.sh"

找到 PID 后，就可以使用 kill PID 来删除该后台进程。

2. 以下命令在后台执行 root 目录下的 yeqiongzhou.sh 脚本，并重定向输入到 yeqiongzhou.log 文件：

> nohup /root/test.sh > yeqiongzhou.log 2>&1 &

### Tips

**2>&1**：将标准错误 2 重定向到标准输出 &1 ，标准输出 &1 再被重定向输入到 runoob.log 文件中。

- 0 – stdin (standard input，标准输入)
- 1 – stdout (standard output，标准输出)
- 2 – stderr (standard error，标准错误输出)
