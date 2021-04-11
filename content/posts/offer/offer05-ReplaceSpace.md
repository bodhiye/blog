---
title: "剑指offer05-替换空格"
date: 2021-04-12T00:05:00+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

## 题目描述

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

## 示例

``` bash
输入：s = "We are happy."
输出："We%20are%20happy."
```

## 限制

`0 <= s 的长度 <= 10000`

## 题解

　　对于 golang 语言来说，字符串被设计成不可变类型，所以需要初始化一个新的字符数组，然后依次往新的字符数组中 append 字符。但是这种方式需要空间复杂度为 O(N)。
　　如果面试官要求一种空间复杂度为 O(1) 的算法时，我们只能使用 C++ 来实现这道题，C++ 的字符串被设计成可变的类型，因此可以在不创建新的字符串情况下实现原地修改。
　　原地修改算法流程：

1. 初始化空格数量 count，字符串长度 length。
2. 统计字符串中空格的数量 count。
3. 修改字符串的长度为 len + 2 * count。
4. 倒序遍历修改字符串的值。

## Tips

　　原地修改算法中必须要从后向前修改，如果从前往后修改的话，每次添加元素都要将后面的元素往后移动。
　　很多数组填充类的问题，都可以先预先给数组扩容带填充后的大小，然后在从后向前进行操作。

## 源码

### golang 实现

```go
package main

import "fmt"

func main() {
	s := "We are happy."
	fmt.Println(replaceSpace(s))
}

func replaceSpace(s string) string {
	var res = make([]byte, 0)
	for i := range s {
		if s[i] == ' ' {
			res = append(res, '%', '2', '0')
		} else {
			res = append(res, s[i])
		}
	}
	return string(res)
}
```

### c++ 实现

```c++
#include <iostream>

using namespace std;

char a[1001];

string replaceSpace(string s)
{
	int count = 0;
	int length = s.size();
	for (int i = 0; i < length; i++)
		if (s[i] == ' ')
			count++;
	int len = length + count * 2;
	s.resize(len);
	while (length--)
	{
		if (s[length] == ' ')
			s[--len] = '0', s[--len] = '2', s[--len] = '%';
		else
			s[--len] = s[length];
	}
	return s;
}

int main()
{
	ios::sync_with_stdio(false);
	string s = "We are happy.";
	cout << replaceSpace(s) << endl;
	return 0;
}
```
