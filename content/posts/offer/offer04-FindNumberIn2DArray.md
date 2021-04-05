---
title: "剑指offer04-二维数组中的查找"
date: 2021-04-05T23:52:00+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

## 题目描述

　　在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

### 示例

现有矩阵 matrix 如下：

```bash
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

给定 target = `5`，返回 `true`。
给定 target = `20`，返回 `false`。

### 限制

`0 <= n <= 1000`
`0 <= m <= 1000`

## 题解

　　首先题目中要求设计一个高效的算法，那肯定不能直接遍历整个数组，如果在面试中被问到这个题目，面试官也不期待见到暴力搜索的解法。
　　由于给定的二维数组具备每行从左到右递增以及每列从上到下递增的特点，所以每行的最后一个元素是在本行最大的元素且在本列最小的元素，通过访问这个元素，可以排除本行或者本列的其它元素。
　　从二维数组的右上角开始查找。如果当前元素等于目标值，则返回 true。如果当前元素大于目标值，则移到左边一列。如果当前元素小于目标值，则移到下边一行。
　　用题目中给的例子来模拟寻找`20`的过程：

```bash
1  4  7  11[15]
2  5  8  12 19
3  6  9  16 22
10 13 14 17 24
18 21 23 26 30

20比15大

2  5  8  12[19]
3  6  9  16 22
10 13 14 17 24
18 21 23 26 30

20比19大

3  6  9  16[22]
10 13 14 17 24
18 21 23 26 30

20比22小

3  6  9 [16]
10 13 14 17
18 21 23 26

20比16大

10 13 14[17]
18 21 23 26

20比17大

18 21 23 [26]

20比26小

18 21 [23]

20比23小

18 [21]

20比21小

[18]

20不等于18，故数组中不含有20，返回false。
```

## 源码

```go
package main

import "fmt"

func main() {
	var matrix = [][]int{
		{1, 4, 7, 11, 15},
		{2, 5, 8, 12, 19},
		{3, 6, 9, 16, 22},
		{10, 13, 14, 17, 24},
		{18, 21, 23, 26, 30},
	}

	fmt.Println(findNumberIn2DArray(matrix, 5))
	fmt.Println(findNumberIn2DArray(matrix, 20))
}

func findNumberIn2DArray(matrix [][]int, target int) bool {
	if matrix == nil || len(matrix) <= 0 || len(matrix[0]) <= 0 {
		return false
	}

	n, m := len(matrix), len(matrix[0])
	for i, j := 0, m-1; i < n && j >= 0; {
		if matrix[i][j] == target {
			return true
		} else if matrix[i][j] < target {
			i++
		} else {
			j--
		}
	}

	return false
}
```

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
