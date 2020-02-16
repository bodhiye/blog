---
title: "Docker部署Golang Http服务"
date: 2020-02-15T22:31:00+08:00
draft: false
categories: ["Golang实战"]
tags: ["Docker", "Golang"]
---

### 前言

最近在工作中有这么一个需求：由于某个服务只在生产环境下部署，测试环境下没有相关服务，但是本地无法访问生产环境的服务，所以我需要mock一个返回特定json的http服务。

#### 服务代码

相关代码已经上传至GitHub：`https://github.com/bodhiye/http-fake`

main.go代码

```go
package main

import (
	"encoding/json"
	"fmt"
	"net/http"
)

type fakeReq struct {
	URI string `json:"uri"`
}

// 处理application/json类型的POST请求
func fake(w http.ResponseWriter, r *http.Request) {
	// 根据请求body创建一个json解析器实例
	decoder := json.NewDecoder(r.Body)
	// 用于存放参数数据
	var req fakeReq
	// 解析参数 存入map
    decoder.Decode(&req)
    // 打印日志
	fmt.Printf("url=%s\n", req.URI)

    // 返回你需要的json，这里返回了{"code": 200}
	fmt.Fprintf(w, `{"code": 200}`)
}

func main() {
	http.HandleFunc("/fake", fake)
	http.ListenAndServe(":2333", nil)
}
```

Dockerfile代码

```dockerfile
FROM golang:latest
MAINTAINER "yeqiongzhou@whu.edu.cn"
WORKDIR /go/src/http-fake
ADD . /go/src/http-fake
RUN go build .
EXPOSE 2333
ENTRYPOINT ["./http-fake"]
```

#### 部署流程

1. 编译Dockerfile文件：`docker build -t bodhiye/http-fake .`编译完成后在终端输入`docker images`可以查看刚才编译好的http-fake镜像。
2. 你得注册一个Docker Hub账号，注册成功后登录Docker Hub：`docker login -u bodhiye`，之后输入密码即可登录成功。
3. 把镜像上传到Docker Hub：`docker push bodhiye/http-fake`上传成功后可以在Docker Hub网站上看到刚刚上传的http-fake镜像。
4. 在你需要部署的服务器或者本地环境下拉取镜像：`docker pull bodhiye/http-fake:latest`代码中latest表示拉取最新的镜像版本。
5. 启动http-fake服务：`docker run --name test-http -d -p 2048:2333 bodhiye/http-fake`将容器服务内部的2333端口映射到本机的2048端口上，并给该容器服务起了一个my-test-http名称。
6. 测试http-fake服务：`curl -X POST -d '{"uri":"https://img.yeqiongzhou.com/test.jpg"}' 127.0.0.1:2048/fake`通过curl的方式来访问本地的http-fake服务，可以看到该服务返回了预期的json字段。如果要在本地访问服务器上的该服务，则127.0.0.1替换成服务器的IP地址。
7. 查看日志：`docker logs test-http`可以打印出服务相关日志`url=https://img.yeqiongzhou.com/test.jpg`