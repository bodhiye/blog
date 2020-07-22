---
title: "ab压力测试"
date: 2020-07-22T07:45:41+08:00
draft: false
categories: ["技能学习"]
tags: ["apache-bench"]
---

### 前言

最近在工作中有这么一个需求：测试原子服务的 QPS 有多少，一种方式是用 Jenkins 跑压力测试，另一种就是今天要用的 apache bench (ab) 测试工具，ab 是用于对 Apache 超文本传输​​协议（HTTP）服务器进行基准测试的工具。

### 压力测试

这里就不展开讲 ab 的语法，直接讲 ab 进行压力测试的命令，详细语法大家可以参考[ab官方文档](https://httpd.apache.org/docs/2.4/programs/ab.html)

在当前目录下新建 *post.json* 文件存放 json 格式的请求
**post.json**: {"data":{"uri":"http://cdn.yeqiongzhou.top/pulp.jpg"}}

> ab -n 60000 -c 60 -p post.json -T application/json -H "Authorization:xxx uid=xxx" "http://12.34.56.78:1024/v1/ab"

下面来详细介绍这条命令，让大家能够快速上手使用。

- -n 6000 代表测试 6000 次
- -c 60 代表模拟了 60 个客户端来请求相应的接口，也就是请求的并发数
- -p 包含了需要 post 的文件地址，和 -T 一起使用
- -H 请求头信息
- 最后跟上要请求的接口地址
