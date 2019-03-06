---
title: "数组中只出现一次的数字"
date: 2019-03-06T19:21:33+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

一个整型数组里除了两个数字之外，其他的数字都出现了偶数次。请写程序找出这两个只出现一次的数字。

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

void FindNumsAppearOnce(vector<int> data, int* num1, int *num2)
{
	int res = 0, index = 0;
	for (int i = 0; i < data.size(); i++)
		res ^= data[i];
	for (int i = 0; i < 32; i++)
		if (res >> i & 1)
		{
			index = i;
			break;
		}
	for (int i = 0; i < data.size(); i++)
	{
		if (data[i] >> index & 1)
			*num1 ^= data[i];
		else
			*num2 ^= data[i];
	}
}

int main()
{
	ios::sync_with_stdio(false);
	vector<int> v;
	int n, temp, num1 = 0, num2 = 0;
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		cin >> temp;
		v.push_back(temp);
	}
	FindNumsAppearOnce(v, &num1, &num2);
	cout << num1 << " " << num2 << endl;
	return 0;
}
```