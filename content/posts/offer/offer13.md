---
title: "剑指offer13——调整数组顺序使奇数位于偶数前面"
date: 2019-03-06T19:19:51+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

void reOrderArray(vector<int> &array)
{
	int begin = 0, from, len = array.size();
	while (begin < len)
	{
		while (begin < len && (array[begin] & 1))
		{
			begin++;
		}
		from = begin + 1;
		while (from < len && !(array[from] & 1))
		{
			from++;
		}
		if (from < len)
		{
			int temp = array[from];
			for (int i = from - 1; i >= begin; i--)
			{
				array[i + 1] = array[i];
			}
			array[begin++] = temp;
		}
		else
		{
			break;
		}
	}
}

int main()
{
	ios::sync_with_stdio(false);
	int n;
	vector<int> v;
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		int temp;
		cin >> temp;
		v.push_back(temp);
	}
	reOrderArray(v);
	for (int i = 0; i < n; i++)
	{
		cout << v[i] << " ";
	}
	cout << endl;
	return 0;
}
```
