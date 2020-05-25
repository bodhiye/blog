---
title: "Linux chgrp命令"
date: 2020-05-25T22:25:47+08:00
draft: false
categories: ["每日Linux命令"]
tags: ["Linux"]
---

---

## 命令详解

Linux chgrp命令用于变更文件或目录的所属群组。
在UNIX系统家族里，文件或目录权限的掌控以拥有者及所属群组来管理。您可以使用chgrp指令去变更文件与目录的所属群组，设置方式采用群组名称或群组识别码皆可。

### 命令全拼

chgrp = change group

### 语法格式

> chgrp [-cfhRv][--help][--version][所属群组][文件或目录...]  
> chgrp [-cfhRv][--help][--reference=<参考文件或目录>][--version][文件或目录...]

### 参数说明

- -c或--changes 效果类似"-v"参数，但仅回报更改的部分。
- -f或--quiet或--silent 不显示错误信息。
- -h或--no-dereference 只对符号连接的文件作修改，而不更动其他任何相关文件。
- -R或--recursive 递归处理，将指定目录下的所有文件及子目录一并处理。
- -v或--verbose 显示指令执行过程。
- --help 在线帮助。
- --reference=<参考文件或目录>　把指定文件或目录的所属群组全部设成和参考文件或目录的所属群组相同。
- --version 显示版本信息。

### 举个栗子

- 改变文件的群组属性:

> chgrp -v bin yeqiongzhou.log

```bash
bodhiye@yeqiongzhou ~/Desktop ll
-rw-r--r-- 1 bodhiye staff 0 May 25 22:05 yeqiongzhou.log
bodhiye@yeqiongzhou ~/Desktop chgrp -v bin yeqiongzhou.log
bodhiye@yeqiongzhou ~/Desktop ll
-rw-r--r-- 1 bodhiye bin 0 May 25 22:05 yeqiongzhou.log
可以看到将yeqiongzhou.log文件由staff群组改为了bin群组。
```

- 根据指定文件改变文件的群组属性:

> chgrp --reference=yeqiongzhou.log xiaofang.log

```bash
bodhiye@yeqiongzhou ~/Desktop ll
-rw-r--r-- 1 bodhiye staff 0 May 25 22:22 xiaofang.log
-rw-r--r-- 1 bodhiye bin   0 May 25 22:05 yeqiongzhou.log
bodhiye@yeqiongzhou ~/Desktop chgrp --reference=yeqiongzhou.log xiaofang.log
bodhiye@yeqiongzhou ~/Desktop ll
-rw-r--r-- 1 bodhiye bin 0 May 25 22:22 xiaofang.log
-rw-r--r-- 1 bodhiye bin 0 May 25 22:05 yeqiongzhou.log
改变文件xiaofang.log 的群组属性，使得文件xiaofang.log的群组属性和参考文件yeqiongzhou.log的群组属性相同。
```
