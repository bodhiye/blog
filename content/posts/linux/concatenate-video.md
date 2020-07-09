---
title: "视频拼接"
date: 2020-06-30T23:16:47+08:00
draft: false
categories: ["技能学习"]
tags: ["FFmpeg"]
---

### 前言

最近在工作中有这么一个需求：用一个超大视频来测试一个视频服务接口，看结果响应是否超时。但是本地只有一个2GB大小的电影文件，如何快速生成一个10GB大小的视频文件。

### 视频拼接

FFmpeg是一套可以用来记录、转换数字音频、视频，并能将其转化为流的开源程序。本文就介绍[FFmpeg官方](https://trac.ffmpeg.org/wiki/Concatenate)推荐的三种视频拼接方法.

1. Concat demuxer: 基于demuxer实现的拼接，需要视频音频的属性完全一样，这种方式不会对视频音频流解码再编码，因此速度很快，推荐大家使用这种方式。

```bash
ffmpeg -f concat -safe 0 -i filelist.txt -c copy yeqiongzhou.mp4
filelist.txt: file 'test1.mp4'
              file 'test1.mp4'
	      file 'test2.mp4'
	      file 'test2.mp4'
通过上面的命令我们就可以通过本地的test1.mp4和test2.mp4这两个小视频文件生成一个大视频文件。
Tips: 如果是相对路径，则不需要上面的-safe 0。
```

2. Concat protocol: 该方式是基于文件来操作的，某些文件（例如MPEG-2 transport streams），这类似于在linux系统上使用cat命令或在Windows上进行复制操作。

> ffmpeg -i "concat:test1.mp4|test2.mp4|test3.mp4" -c copy yeqiongzhou.mp4

3. Concat filter: 这种方式实际上是把所有的视频音频全部解码，统一为原始的音视频流，然后塞进编码器重新编码。这种方式需要视频之间的分辨率和帧率必须一致，优点是兼容性好，能够应付绝大部分场景。

```bash
ffmpeg -i test1.mp4 -i test2.webm -i test3.mov \
-filter_complex "[0:v:0][0:a:0][1:v:0][1:a:0][2:v:0][2:a:0]concat=n=3:v=1:a=1[outv][outa]" \
-map "[outv]" -map "[outa]" yeqiongzhou.mkv
通过上面的命令我们合并了三个具有视频流和音频流的文件。
```
