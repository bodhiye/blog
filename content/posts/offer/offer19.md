---
title: "顺时针打印矩阵"
date: 2019-03-06T19:20:16+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

vector<int> printMatrix(vector<vector<int> > matrix)
{
	vector<int> res;
	int row = matrix.size(), col = matrix[0].size();
	int circle = ((row < col ? row : col) + 1) / 2;
	for (int i = 0; i < circle; i++)
	{
		for (int j = i; j < col - i; j++)
			res.push_back(matrix[i][j]);
		for (int k = i + 1; k < row - i; k++)
			res.push_back(matrix[k][col - i - 1]);
		for (int m = col - i - 2; (m >= i) && (row - i - 1 != i); m--)
			res.push_back(matrix[row - i - 1][m]);
		for (int n = row - i - 2; (n > i) && (col - i - 1 != i); n--)
			res.push_back(matrix[n][i]);
	}
	return res;
}

int main()
{
	ios::sync_with_stdio(false);
	vector<vector<int> > vv;
	vector<int> res, v;
	int n, m, temp;
	cin >> n >> m;
	for (int i = 0; i < n; i++)
	{
		v.clear();
		for (int j = 0; j < m; j++)
		{
			cin >> temp;
			v.push_back(temp);
		}
		vv.push_back(v);
	}
	res = printMatrix(vv);
	vector<int>::iterator it;
	for (it = res.begin(); it != res.end(); it++)
		cout << *it << " ";
	cout << endl;
	return 0;
}
```