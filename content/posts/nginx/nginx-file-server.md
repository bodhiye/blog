---
title: "Nginx 搭建离线文件服务器"
date: 2021-03-15T23:26:14+08:00
categories: ["Nginx 实战"]
tags: ["Nginx"]
---

### 前言

　　最近在工作中有这么一个需求：我们给客户部署服务的机器不能访问外网，导致我们某个服务不能拉取公网图片资源。为了验证整套服务流程是否连通，只能在目标机器上部署一个文件服务器来代替公网资源来测试整套服务。

### 部署 nginx 文件服务器

#### 离线安装 nginx

1. 联网机器上下载 nginx 安装包。
2. 安装包拷贝到目标服务器，安装 nginx，`dpkg -i nginx_xxx.deb`。
3. 查看 nginx 安装路径，`whereis nginx`。
4. 启动 nginx。

#### 修改配置文件

　　nginx 会将 conf.d 文件夹下的 *.conf 文件全部自动引入到配置文件中，所以我们在 conf.d 文件夹下新建一个 file_server.conf 配置文件。

``` bash
server {
  listen 80; # 80 端口，这里注意端口是否被占用
  server_name localhost; # 主机名，这里选择本机
  root /home/file; # 文件服务器的文件存放目录
  location / {
    autoindex on; # 显示索引
    autoindex_exact_size on; # 显示大小
    autoindex_localtime on; # 显示时间
    charset utf-8; # 避免中文乱码
  }
}
```

　　接下来需要删除 nginx 的默认配置：`cp /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf.bak`。启动 nginx 服务：`/etc/init.d/nginx start`。

#### 测试文件服务器

1. 往文件服务器拷贝本地图片。
2. 查看服务器内网地址：`hostname -I`。
3. 通过内网地址访问图片链接：`http://10.10.100.100/xxx.jpg`。
