---
title: "组合"
date: 2020-10-26T23:32:21+08:00
draft: false
categories: ["Leetcode题解"]
tags: ["Leetcode"]
---

---

## 题目描述

给定两个整数 n 和 k，返回 1 ... n 中所有可能的 k 个数的组合。

### 示例

``` html
输入: n = 4, k = 2
输出:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

## 题解

``` go
package main

import "fmt"

func main() {
	fmt.Print(combine(4, 2))
}

func combine(n int, k int) (ans [][]int) {
	tmp := []int{}
	var dfs func(int)
	dfs = func(cur int) {
		// 剪枝
		if len(tmp)+(n-cur+1) < k {
			return
		}
		if len(tmp) == k {
			comb := make([]int, k)
			copy(comb, tmp)
			ans = append(ans, comb)
			return
		}
		// 选择当前位置
		tmp = append(tmp, cur)
		dfs(cur + 1)
		// 不选择当前位置
		tmp = tmp[:len(tmp)-1]
		dfs(cur + 1)
	}
	dfs(1)
	return
}
```
