---
title: "无重复字符的最长子串"
date: 2020-05-25T23:21:21+08:00
draft: false
categories: ["每日算法"]
tags: ["Leetcode"]
---

---

## 题目描述

给定一个字符串，请你找出其中不含有重复字符的最长子串的长度。

### 示例 1:

```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

### 示例 2:

```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

### 示例 3:

```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

## 题解

```golang
package main

import (
	"fmt"
)

func main() {
	str := []string{"abcabcbb", "bbbbb", "pwwkew"}
	for _, s := range str {
		len := lengthOfLongestSubstring(s)
		fmt.Println(len)
	}
}

func lengthOfLongestSubstring(s string) int {
	lastOccurred := make(map[byte]int)
	start := 0
	maxLength := 0
	for i, ch := range []byte(s) {
		if lastI, ok := lastOccurred[ch]; ok && lastI >= start {
			start = lastI + 1
		}
		if i-start+1 > maxLength {
			maxLength = i - start + 1
		}
		lastOccurred[ch] = i
	}
	return maxLength
}
```
