---
title: "不同路径"
date: 2020-07-30T00:23:29+08:00
draft: false
categories: ["Leetcode题解"]
tags: ["Leetcode"]
---

---

## 题目描述

一个机器人位于一个 m x n 网格的左上角（起始点在下图中标记为“Start” ）。
机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。
问总共有多少条不同的路径？

![不同路径](http://blog.yeqiongzhou.com/unique-paths-ii.jpg)

例如，上图是一个 7 x 3 的网格，有多少可能的路径？

### 示例 1:

``` html
输入: m = 3, n = 2
输出: 3
解释: 从左上角开始，总共有 3 条路径可以到达右下角。

1. 向右 -> 向右 -> 向下
2. 向右 -> 向下 -> 向右
3. 向下 -> 向右 -> 向右

```

### 示例 2:

``` html
输入: m = 7, n = 3
输出: 28
```

### 提示

* 1 <= m, n <= 100
* 题目数据保证答案小于等于 2 * 10 ^ 9

## 题解

``` golang
package main

import (
	"fmt"
)

func main() {
	len := uniquePaths(2,3)
	fmt.Println(len)
}

func uniquePaths(m, n int) int {
	f := make([]int, m)
	f[0] = 1
	for i := 0; i < n; i++ {
		for j := 0; j < m; j++ {
			if j-1 >= 0 {
				f[j] += f[j-1]
			}
		}
	}
	return f[len(f)-1]
}
```
