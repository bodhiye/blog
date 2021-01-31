---
title: "剑指offer11——二进制中1的个数"
date: 2019-03-06T19:19:42+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

#### 题解

```c++
#include <iostream>

using namespace std;

int  NumberOf1(int n)
{
	int count = 0;
	while (n != 0)
	{
		count++;
		n = n & (n - 1);
	}
	return count;
}

int main()
{
	ios::sync_with_stdio(false);
	int n;
	cin >> n;
	cout << NumberOf1(n) << endl;
	return 0;
}
```
