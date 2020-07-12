---
title: "Dockerfile多阶段构建"
date: 2020-07-12T23:33:47+08:00
draft: false
categories: ["Docker手册"]
tags: ["Docker"]
---

### 前言

我们在构建docker镜像时，希望最后得到的镜像越小越好，但是在构建时，总是会用到各种各样复杂的环境，大部分都是临时环境，只是为了生成对应的目标程序。比如我们经常会在OpenCV环境下编译图像处理类程序，但其实目标程序只需要用的之前生成的子程序就行，不需要引入中间用到的环境。这里我们就能用到Dockerfile多阶段构建，它可以把前面多个阶段生成的文件拷贝到下一个阶段使用，并且不引入之前用到的环境，这极大地解耦了我们的Dockerfile文件，而且最终可以得到一个极小的完整镜像。

### 多阶段构建

关于镜像构建，最重要的事情之一就是让镜像容量尽可能的变得更小，Dockerfile中的每条指令都会添加一层镜像，我们需要在进入下一层时清除之后用不到的文件。
在多阶段构建中，我们可以通过`FROM`指令在Dockerfile中生成多个阶段。每个FROM指令可以使用不同的base镜像，并且每个指令都开始构建的新阶段，您可以把前一个阶段生成的文件COPY到另一个阶段，从而在最终的镜像中只留下需要的所有内容，下面通过一个例子来实践一下多阶段构建的方法。

```html
FROM golang:1.10.2
WORKDIR /go/src/github.com/yeqiongzhou/docker-multistage-build/
RUN go get -d -v golang.org/x/net/html
COPY app.go .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=0 /go/src/github.com/yeqiongzhou/docker-multistage-build/app .
CMD ["./app"]
```

通过build上面的Dockerfile文件，我们可以得到一个微型的镜像，第二条FROM指令以`alpine:latest`镜像作为基础镜像开始新的构建阶段，`COPY --from=0`命令可以将之前阶段的文件复制到这个新阶段。Golang SDK和其它临时文件都留在了第一个stage，没有保存到最终的镜像中，这极大的降低了Dockerfile的复杂度和减小了镜像的大小。

### 多阶段构建的命名

默认情况下，未命名的阶段，您可以通过其整数编号来引用它们，第一FROM条指令的起始编号为0。但是，您还可以通过`AS <NAME>`在FROM指令中添加来命名阶段。下面的示例通过给阶段命名并在COPY指令中使用名称来引用前一个阶段的文件。这意味着，即使以后对Dockerfile中的指令进行了重新排序，它们也能正常的构建运行。

```html
FROM golang:1.10.2 AS yeqiongzhou
WORKDIR /go/src/github.com/yeqiongzhou/docker-multistage-build/
COPY app.go .
RUN go get -d -v golang.org/x/net/html && \
    CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=yeqiongzhou /go/src/github.com/yeqiongzhou/docker-multistage-build/app .
CMD ["./app"]
```

### 构建指定的阶段

构建映像时，不必构建整个Dockerfile，即所有的阶段。您可以指定目标构建阶段。以上面的Dockerfile为例，我们可以通过以下命令只构建第一个阶段。
> docker build --target yeqiongzhou -t yeqiongzhou/docker-multistage-build:latest .
这个方法可以在调试测试阶段发挥很大的作用。

### 拷贝外部镜像的文件

使用多阶段构建时，您不仅可以之前在Dockerfile中创建的阶段进行拷贝。您可以使用`COPY --from`指令从外部的镜像进行拷贝操作。
> COPY --from=nginx:latest /etc/nginx/nginx.conf /nginx.conf

#### 注

Dockerfile中`&&`运算符可以人为地将两个命令压缩在一起，以避免在镜像中创建额外的镜像层。另外如果命令比较长时不要忘记使用`\`字符分隔命令行。
