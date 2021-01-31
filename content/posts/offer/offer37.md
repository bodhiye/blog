---
title: "剑指offer37——数字在排序数组中出现的次数"
date: 2019-03-06T19:21:19+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

统计一个数字在排序数组中出现的次数。

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

int binarySearch(vector<int> data, int left, int right, int k)
{
	while (left <= right)
	{
		int mid = (left + right) >> 1;
		if (k == data[mid])
			return mid;
		else if (k < data[mid])
			right = mid - 1;
		else
			left = mid + 1;
	}
	return -1;
}

int getNumberOfK(vector<int> data, int k)
{
	int sum = 1;
	int len = data.size();
	if (!len) return 0;
	int index = binarySearch(data, 0, len - 1, k);
	if (index == -1) return 0;
	int left = index - 1, right = index + 1;
	while (left >= 0 && data[left] == k)
	{
		left--;
		sum++;
	}
	while (right < len&&data[right] == k)
	{
		right++;
		sum++;
	}
	return sum;
}

int main()
{
	std::ios::sync_with_stdio(false);
	vector<int> v;
	int n, k, temp;
	cin >> n;
	for (int i = 1; i <= n; i++)
	{
		cin >> temp;
		v.push_back(temp);
	}
	cin >> k;
	cout << getNumberOfK(v, k) << endl;
	return 0;
}
```
