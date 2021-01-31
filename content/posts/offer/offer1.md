---
title: "剑指offer1——二维数组中的查找"
date: 2019-03-06T19:10:30+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

bool find(int target, vector<vector<int> > array)
{
	int rows = array.size(), cols = array[0].size();
	int i = rows - 1, j = 0;
	while (i >= 0 && j < cols)
	{
		if (target < array[i][j])
			i--;
		else if (target > array[i][j])
			j++;
		else
			return true;
	}
	return false;
}

int main()
{
	ios::sync_with_stdio(false);
	vector<vector<int> > array;
	vector<int> v;
	int m, n, target, temp;
	cin >> m >> n >> target;
	for (int i = 0; i < m; i++)
	{
		for (int j = 0; j < n; j++)
		{
			cin >> temp;
			v.push_back(temp);
		}
		array.push_back(v);
		v.clear();
	}
	cout << find(target, array) << endl;
	return 0;
}
```
