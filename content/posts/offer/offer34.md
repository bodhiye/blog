---
title: "剑指offer——34第一个只出现一次的字符位置"
date: 2019-03-06T19:21:10+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

在一个字符串(0<=字符串长度<=10000，全部由字母组成)中找到第一个只出现一次的字符,并返回它的位置, 如果没有则返回 -1（需要区分大小写）.

#### 题解

```c++
#include <iostream>
#include <string>
#include <map>

using namespace std;

int FirstNotRepeatingChar(string str)
{
	map<char, int> m;
	for (int i = 0; i < str.length(); i++)
		m[str[i]]++;
	for (int i = 0; i < str.length(); i++)
	{
		if (m[str[i]] == 1)
			return i;
	}
	return -1;
}

int main()
{
	ios::sync_with_stdio(false);
	string s;
	cin >> s;
	cout << FirstNotRepeatingChar(s) << endl;
	return 0;
}
```
