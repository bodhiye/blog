---
title: "剑指offer50-第一个只出现一次的字符"
date: 2021-04-30T22:23:00+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

## 题目描述

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

## 示例

s = "abaccdeff"
返回 "b"

s = ""
返回 " "

## 限制

`0 <= s 的长度 <= 50000`

## 题解

　　这题最直观的解法是使用哈希 map 存储每个字符的出现次数，字符作为 key，出现次数为 value。遍历两次字符串，第一次遍历记录每个字符出现次数，第二次遍历找出次数为 1 的字符，如果没有则返回' '。
　　由于考虑到字符串只包含 26 个小写字母，在 golang 中，当数据量比较少时，slice 空间占用和查找效率比 map 都要好，可以使用整型数组来存储每个字符出现的次数。

## 源码

### golang 实现

```go
package main

import "fmt"

func main() {
	fmt.Println(firstUniqChar("leetcode"))
}

func firstUniqChar(s string) byte {
	ss := make(map[rune]int)
	for _, c := range s {
		ss[c]++
	}
	for _, c := range s {
		if ss[c] == 1 {
			return byte(c)
		}
	}
	return ' '
}

func firstUniqChar1(s string) byte {
	ss := [26]int{}
	for _, c := range s {
		ss[c-'a']++
	}
	for _, c := range s {
		if ss[c-'a'] == 1 {
			return byte(c)
		}
	}
	return ' '
}
```

### c++ 实现

```c++
#include <iostream>
#include <string>
#include <map>

using namespace std;

char firstUniqChar(string s)
{
    map<char, int> m;
    for (int i = 0; i < s.length(); i++)
        m[s[i]]++;
    for (int i = 0; i < s.length(); i++)
        if (m[s[i]] == 1)
            return s[i];
    return ' ';
}

int main()
{
    ios::sync_with_stdio(false);
    cout << firstUniqChar("abaccdeff") << endl;
    return 0;
}
```
