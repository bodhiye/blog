---
title: "剑指offer9——变态跳台阶"
date: 2019-03-06T19:19:33+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

#### 题解

```c++
#include <iostream>

using namespace std;

int jumpFloor(int number)
{
	return 1 << --number;
}

int main()
{
	ios::sync_with_stdio(false);
	int n;
	cin >> n;
	cout << jumpFloor(n) << endl;
	return 0;
}
```
