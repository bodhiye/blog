---
title: "数组中的逆序对"
date: 2019-03-06T19:21:13+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组,求出这个数组中的逆序对的总数P。并将P对1000000007取模的结果输出。 即输出P%1000000007

#### 输入描述:

题目保证输入的数组中没有的相同的数字

数据范围：
	对于%50的数据,size<=10^4
	对于%75的数据,size<=10^5
	对于%100的数据,size<=2*10^5

#### 示例1

输入

1,2,3,4,5,6,7,0

输出

7

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

int temp[200001];
long long cnt = 0;

void merge(vector<int> &a, int start, int mid, int end)
{
	int i = start, j = mid + 1, index = 0;
	while (i <= mid && j <= end)
	{
		if (a[i] <= a[j])
			temp[index++] = a[i++];
		else
		{
			cnt += (mid - i + 1);
			temp[index++] = a[j++];
		}
	}
	while (i <= mid)temp[index++] = a[i++];
	while (j <= end)temp[index++] = a[j++];
	for (int i = 0; i < index; i++)
		a[start + i] = temp[i];
}

void mergesort(vector<int> &data, int start, int end)
{
	if (start < end)
	{
		int mid = (start + end) >> 1;
		mergesort(data, start, mid);
		mergesort(data, mid + 1, end);
		merge(data, start, mid, end);
	}
}

int InversePairs(vector<int> data)
{
	int len = data.size();
	if (!len)return 0;
	mergesort(data, 0, len - 1);
	return cnt % 1000000007;
}

int main()
{
	ios::sync_with_stdio(false);
	vector<int> a;
	int n, tmp;
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		cin >> tmp;
		a.push_back(tmp);
	}
	cout << InversePairs(a) << endl;
	return 0;
}
```