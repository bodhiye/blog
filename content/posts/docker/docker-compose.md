---
title: "Docker Compose 详解"
date: 2021-01-02T20:13:14+08:00
draft: false
categories: ["Docker手册"]
tags: ["Docker"]
---

### 前言

　　当我们想要同时启动一系列相互依赖的服务时，一个个依次并严格按照顺序启动就显得尤为繁琐。这时我们就可以用到 docker compose 来执行这一系列操作。

### Compose

　　Compose 是用于定义和运行多容器 Docker 应用程序的工具。通过 Compose 您可以使用 YML 文件来配置应用程序需要的所有服务，然后使用一个命令就可以从 YML 文件配置中创建并启动所有服务。

### Compose 使用

* 使用 Dockerfile 定义应用程序的环境。
* 使用 docker-compose.yml 定义构成应用程序的服务，这样它们可以在隔离环境中一起运行。
* 最后执行 docker-compose up 命令来启动并运行整个应用程序。

#### demo Dockerfile

``` Dockerfile
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP app.py
ENV FLASK_RUN_HOST 0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
COPY . .
CMD ["flask", "run"]
```

* `FROM python:3.7-alpine`: 从 Python 3.7 基础镜像开始构建镜像。
* `WORKDIR /code`: 将工作目录设置为 /code。
* `ENV FLASK_APP app.py`、`ENV FLASK_RUN_HOST 0.0.0.0`: 设置环境变量。
* `COPY requirements.txt requirements.txt`、`RUN pip install -r requirements.txt`: 复制 requirements.txt 并安装 Python 依赖项。
* `COPY . .`: 将 . 项目中的当前目录复制到 . 镜像中的工作目录。
* `CMD ["flask", "run"]`: 容器提供默认的执行命令为：flask run。

#### docker-compose.yml

``` yml
version: "3"
services:
  mongo:
    image: mongo:3.4.24-xenial
    command: mongod --port 27017
    ports:
      - "27017:27017"
  demo:
    build: .
    ports:
      - "5000:5000"
    depends_on:
      - mongo
```

#### 构建和运行服务

`docker-compose up` ，如果您想在后台运行的话后面跟上 `-d` 参数。

### yml 配置参考

#### version

`version: "3"` 指定本 yml 依从的 compose 哪个版本制定的。

#### build

指定构建的参数

``` yml
version: "3"
services:
  demo:
    build:
      context: ./dir
      dockerfile: demo/Dockerfile
      args:
        buildno: 1
      labels:
        - "com.example.description=yeqiongzhou demo"
        - "com.example.department=China Shanghai"
        - "com.example.label-with-empty-value"
      target: prod
```

* context: 上下文路径。
* dockerfile: 指定构建镜像的 Dockerfile 文件名。
* args: 添加构建参数，这是只能在构建过程中访问的环境变量。
* labels: 设置构建镜像的标签。
* target: 多层构建，可以指定构建哪一层。

#### command

`command: ["go", "run", "main.go"]` 会覆盖 Dockerfile 容器中指定的默认命令。

#### container_name

`container_name: yeqiongzhou-demo` 指定自定义容器名称，而不是生成的默认名称。

#### depends_on

设置依赖关系。

* docker-compose up: 以依赖性顺序启动服务。在以下示例中，先启动 db 和 redis ，才会启动 demo。
* docker-compose up SERVICE ：自动包含 SERVICE 的依赖项。在以下示例中，docker-compose up demo 还将创建并启动 db 和 redis。
* docker-compose stop ：按依赖关系顺序停止服务。在以下示例中，demo 在 db 和 redis 之前停止。

``` yml
version: "3"
services:
  demo:
    build: .
    depends_on:
      - db
      - redis
  redis:
    image: redis
  db:
    image: postgres
```

#### entrypoint

`entrypoint: /code/entrypoint.sh` 会覆盖容器默认的 entrypoint。

#### environment

　　添加环境变量。您可以使用数组或字典、任何布尔值，布尔值需要用引号引起来，以确保 YML 解析器不会将其转换为 True 或 False。

``` yml
environment:
  RACK_ENV: development
  SHOW: 'true'
```

#### expose

暴露端口，但不映射到宿主机，只被连接的服务访问，仅可以指定内部端口为参数。

``` yml
expose:
  - "6666"
  - "8888"
```

#### healthcheck

用于检测 docker 服务是否健康运行。

``` yml
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost:8888/health"] # 设置检测程序
  interval: 60s # 设置检测间隔
  timeout: 10s # 设置检测超时时间
  retries: 3 # 设置重试次数
  start_period: 30s # 启动后，多少秒开始启动检测程序
```

#### image

指定容器运行的镜像。以下格式都可以:

* image: golang
* image: ubuntu:18.04
* image: yeqiongzhou/demo
* image: example-registry.com:5000/redis
* image: a4bc65fd # 镜像id

#### logging

　　服务的日志记录配置。driver: 指定服务容器的日志记录驱动程序，默认值为json-file。有以下三个选项:

* driver: "json-file"
* driver: "syslog"
* driver: "none"

　　仅在 json-file 驱动程序下，可以使用以下参数，限制日志的数量和大小。当达到文件限制上限，会自动删除旧的文件。

``` yml
logging:
  driver: json-file
  options:
    max-size: "200k" # 单个文件大小为200k
    max-file: "10" # 最多10个文件
```

syslog 驱动程序下，可以使用 syslog-address 指定日志接收地址。

``` yml
logging:
  driver: syslog
  options:
    syslog-address: "tcp://192.168.0.1:1024"
```

#### restart

* no：是默认的重启策略，在任何情况下都不会重启容器。
* always：容器总是重新启动。
* on-failure：在容器非正常退出时（退出状态非0），才会重启容器。
* unless-stopped：在容器退出时总是重启容器，但是不考虑在Docker守护进程启动时就已经停止了的容器。

#### volumes

将主机的数据卷或者文件挂载到容器里。

``` yml
version: "3"
services:
  db:
    image: postgres:latest
    volumes:
      - "/localhost/postgres.sock:/var/run/postgres/postgres.sock"
      - "/localhost/data:/var/lib/postgresql/data"
```
