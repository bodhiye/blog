---
title: "剑指offer7——斐波那契数列"
date: 2019-03-06T19:19:26+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0）。
n<=39

#### 题解

```c++
#include <iostream>

using namespace std;

int dp[40];

int Fibonacci(int n)
{
	if (n == 0 || n == 1)return n;
	if (dp[n])return dp[n];
	else
		return dp[n] = Fibonacci(n - 1) + Fibonacci(n - 2);
}

int main()
{
	ios::sync_with_stdio(false);
	int n;
	cin >> n;
	cout << Fibonacci(n) << endl;
	return 0;
}
```
