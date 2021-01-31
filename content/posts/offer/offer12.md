---
title: "剑指offer12——数值的整数次方"
date: 2019-03-06T19:19:48+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

#### 题解

```c++
#include <iostream>

using namespace std;

double power(double base, int exponent)
{
	int exp = abs(exponent);
	double ans = 1.0;
	while (exp)
	{
		if (exp & 1)ans *= base;
		base *= base;
		exp >>= 1;
	}
	return exponent < 0 ? 1 / ans : ans;
}

int main()
{
	ios::sync_with_stdio(false);
	double a;
	int b;
	cin >> a >> b;
	cout << power(a, b) << endl;
	return 0;
}
```
