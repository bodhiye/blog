---
title: "替换空格"
date: 2019-03-06T19:15:53+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

#### 题解

```c++
#include <iostream>

using namespace std;

char a[1001];

void replaceSpace(char *str, int length)
{
	int sum = 0;
	for (int i = 0; i < length; i++)
		if (str[i] == ' ')
			sum++;
	int len = length + sum * 2;
	while (length--)
	{
		if (str[length] == ' ')
			str[--len] = '0', str[--len] = '2', str[--len] = '%';
		else
			str[--len] = str[length];
	}
}

int main()
{
	ios::sync_with_stdio(false);
	cin.get(a, 1001);
	int len = strlen(a);
	replaceSpace(a, len);
	cout << a << endl;
	return 0;
}
```