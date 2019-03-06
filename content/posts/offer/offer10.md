---
title: "矩形覆盖"
date: 2019-03-06T19:19:37+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？

#### 题解

```c++
#include <iostream>

using namespace std;

int dp[101];

int rectCover(int number)
{
	if (number < 1)return 0;
	if (number == 1 || number == 2)return number;
	if (dp[number])return dp[number];
	else
		return dp[number] = rectCover(number - 1) + rectCover(number - 2);
}

int main()
{
	ios::sync_with_stdio(false);
	int n;
	cin >> n;
	cout << rectCover(n) << endl;
	return 0;
}
```