---
title: "Linux chattr命令"
date: 2019-12-18T08:40:47+08:00
draft: false
categories: ["每日Linux命令"]
tags: ["Linux"]
---

---

## 命令详解

chattr 命令用于改变文件属性。
这项指令可改变存放在 ext2 文件系统上的文件或目录属性，这些属性共有以下8种模式:

- a：append only，让文件或目录仅供附加用途，设定该参数后，只能向文件中添加数据，而不能删除，多用于服务器日志文件安全。
- A：no atime updates，不更新文件或目录的最后存取时间，文件或目录的 atime (access time)不可被修改(modified)。
- c：compressed，将文件或目录压缩后存放，设定文件是否经压缩后再存储，读取时需要经过自动解压操作将文件或目录压缩后存放。
- C：no copy-on-write (COW)，不执行写入时复制，多个调用者获取同一个资源，这时另一个调用者对这资源进行了修改，不生成一个副本。
- d：no dump，将文件或目录排除在倾倒操作之外，设定文件不能成为 dump 程序的备份目标。
- D：synchronous directory updates，同步更新目录。
- e：extent format，extent 格式。
- i：immutable，不得任意更动文件或目录，设定文件不能被删除、改名、设定链接关系，同时不能写入或新增内容。
- j：data journaling，数据日志，文件在写入时会先被记录。
- s：secure deletion，保密性删除文件或目录，即硬盘空间被全部收回。
- S：synchronous updates，即时更新文件或目录，功能类似 sync。
- t：no tail-merging，文件系统支持尾部合并。
- T：top of directory hierarchy，具有该属性的目录将被视为目录层次结构的顶部。
- u：undeletable，预防意外删除，与s相反，当设定为u时，数据内容其实还存在磁盘中

### 命令全拼
chattr = change attributes

### 语法格式

> chattr [-RVf] [-+=aAcCdDeijsStTu] [-v version] files...

### 参数说明

- -R 递归处理，将指定目录下的所有文件及子目录一并处理。
- -v<版本编号> 设置文件或目录版本。
- -V 显示指令执行过程。
- +<属性> 开启文件或目录的该项属性。
- -<属性> 关闭文件或目录的该项属性。
- =<属性> 指定文件或目录的该项属性。

### 举个栗子

- 用 chattr 命令防止系统中某个关键文件被修改:

> chattr +i /root/yeqiongzhou.yaml
> lsattr /root/yeqiongzhou.yaml

会显示如下属性:
`----i-------- /root/yeqiongzhou.yaml`

- 让某个文件只能往里面追加数据，但不能删除，适用于各种日志文件:

> chattr +a /var/log/messages

#### 注

- 各参数选项中常用到的是a和i。a选项强制只可添加不可删除，多用于日志系统的安全设定。而i是更为严格的安全设定，只有superuser (root) 或具有 CAP_LINUX_IMMUTABLE 处理能力（标识）的进程能够施加该选项。
