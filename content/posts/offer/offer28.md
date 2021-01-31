---
title: "剑指offer28——数组中出现次数超过一半的数字"
date: 2019-03-06T19:20:47+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

int MoreThanHalfNum_Solution(vector<int> numbers)
{
	int len = numbers.size();
	int count = 0, ans;
	for (int i = 0; i < len; i++)
	{
		if (!count)
		{
			ans = numbers[i];
			count = 1;
		}
		else
		{
			if (ans == numbers[i])
				count++;
			else
				count--;
		}
	}
	count = 0;
	for (int i = 0; i < len; i++)
		if (numbers[i] == ans)count++;
	if (count * 2 > len)
		return ans;
	return 0;
}

int main()
{
	ios::sync_with_stdio(false);
	int n, temp;
	vector<int> v;
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		cin >> temp;
		v.push_back(temp);
	}
	cout << MoreThanHalfNum_Solution(v) << endl;
	return 0;
}
```
