---
title: "git cherry-pick命令"
date: 2020-11-29T22:13:14+08:00
draft: false
categories: ["git手册"]
tags: ["git"]
---

---

### 前言

在我们日常开发的时候，经常会在不同的分支上切换出新的分支进行编码，当不小心切错了基准分支时，最后代码合并的时候可能会有冲突，或者是仅仅需要把某个分支的内容合并到另外的分支上时，我们就需要使用到 Cherry-Pick 功能了。

## 命令详解

cherry-pick 是 Git 版本控制工具中的一个命令，意思和它的名称一样，精心挑选，挑选一个我们需要的 commit 进行操作。它可以用于将在其他分支上的 commit 修改，移植到当前的分支。

一个很常见的场景，就是想在某个稳定版本上，添加一个刚开发完成的版本中的功能。就可以使用 Cherry-pick 命令，将这个功能相关的 commit 提取出来，合入稳定版本的分支上。

### 语法格式

> git cherry-pick [--edit] [-n] [-m parent-number] [-s] [-x] [--ff] [-S[<keyid>]] <commit>...

### 举个栗子

1、 把 v2 分支上的 commit 提交到 v1 分支上：

- 在 v2 分支上查看提交的 commit: `$ git log`
- 切换到 v1 分支 `$ git checkout v1`
- 将位于 v2 分支上的 1a2b3c4d 提交合并到 v1: `$ git cherry-pick 1a2b3c4d`
- 当执行完 Cherry Pick 之后，将会生成一个新的提交

2、 同时合并多个 commit：

- 新版本的 git 支持批量 cherry-pick: `$ git cherry-pick <start-commit-id>…<end-commit-id>`
- 可以一次将一个连续的时间序列内的 commit，设定一个开始和结束的 commit，进行 cherry-pick 操作，但是它是一个 (左开，右闭] 的区间
- 如果想要包含 start-commit-id 的话，就需要使用 ^ 标记一下，就会变成一个 [左闭，右闭] 的区间: `$ git cherry-pick <start-commit-id>^…<end-commit-id>`

### Tips

无论是对单个 commit 进行 cherry-pick，还是批量处理，注意一定要根据时间线，依照 commit 的先后顺序来处理，否者会有意想不到的问题。
