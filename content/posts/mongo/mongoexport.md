---
title: "mongo导出数据"
date: 2020-06-30T23:55:47+08:00
draft: false
categories: ["数据库详解"]
tags: ["MongoDB"]
---

### 前言

最近工作上遇到一个需求，需要给算法人员导出某天某个用户所有的数据，这里就要用到mongoexport命令了。

### 导出数据

> mongoexport -h your-mongo-hostname --port 27017 -d database-name -c collection-name -q '{"uid":123456, "created_at":{$gt:Date(1593446400000)}}' -o /home/yeqiongzhou/test.json

该命令可以通过查询条件导出指定用户(123456)在指定时间(2020-06-30)后的所有记录
Tips: -q选项可以指定查询条件，但是时间不支持ISODate格式，所以必须将时间转换为毫秒，可以通过`date -d 2020-06-30 +%s`将ISODate格式的时间转换为时间戳，然后补上三个0转换为毫秒。
