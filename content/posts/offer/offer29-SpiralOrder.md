---
title: "剑指offer29-顺时针打印矩阵"
date: 2021-04-26T00:23:00+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

## 题目描述

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

## 示例

示例 1：

输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]

示例 2：

输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]

## 限制

`0 <= matrix.length <= 100`
`0 <= matrix[i].length <= 100`

## 题解

### 模拟

　　遇到这种问题首先能想到的就是模拟，模拟打印出矩阵的路径，初始化四个方向（向右->向下->向左->向上），依次按照顺时针来访问矩阵节点，当超出边界或者遇到之前已经访问过的节点时就进入下一个方向，所以需要初始化一个和原始矩阵大小相等的辅助矩阵 visited 来标记当前节点是否被访问过，当前路径的长度等于矩阵的大小时表示模拟结束。时间复杂度和空间复杂度都为 O(m*n)。

### 按层遍历

　　模拟解法最大的问题是需要一个和原始矩阵一样的辅助矩阵，有没有更优的解法呢？当然是有的，我们可以选择直接按层来遍历矩阵，就像剥洋葱一样一层一层来遍历，首先要定要剥洋葱的规则，我们按照顺时针来遍历，首先每层有四个边，依次为（上->右->下->左），我们给每个边设定好遍历的边界就可以不需要辅助矩阵了。
　　假设当前层的左上角位于 (up, left)，右下角位于 (down, right)

```html
上 上 上 上 上
左 里 里 里 右
下 下 下 下 右
```

1. 从左到右遍历上侧元素，依次为 (up, left) 到 (up, right)
2. 从上到下遍历右侧元素，依次为 (up+1, right) 到 (down, right)
3. 这里要判断当前是否 left < right && up < down，否则当单行或者单列成最后一圈时重复遍历，如果条件成立则依次遍历下侧元素 (down, right-1) 到 (down, left) 和左侧元素 (down-1, left) 到 (up+1, left)

　　遍历完当前层的元素之后，将 up 和 left 分别增加 1，将 down 和 right 分别减少 1，进入下一层继续遍历，直到遍历完所有元素为止。

## 源码

### golang 实现

```go
package main

import "fmt"

func main() {
	matrix := [][]int{{1, 2, 3}, {4, 5, 6}, {7, 8, 9}}
	matrix1 := [][]int{{1, 2, 3, 4}, {5, 6, 7, 8}, {9, 10, 11, 12}}
	fmt.Println(spiralOrder(matrix))
	fmt.Println(spiralOrder(matrix1))
	fmt.Println(spiralOrder1(matrix))
	fmt.Println(spiralOrder1(matrix1))
}

func spiralOrder(matrix [][]int) []int {
	if len(matrix) == 0 || len(matrix[0]) == 0 {
		return nil
	}
	m, n := len(matrix), len(matrix[0])
	visited := make([][]bool, m)
	for i := 0; i < m; i++ {
		visited[i] = make([]bool, n)
	}

	var (
		ret       = make([]int, m*n)
		direc     = [][]int{{0, 1}, {1, 0}, {0, -1}, {-1, 0}}
		x, y, cur = 0, 0, 0
	)

	for i := 0; i < m*n; i++ {
		ret[i] = matrix[x][y]
		visited[x][y] = true
		nextX, nextY := x+direc[cur][0], y+direc[cur][1]
		if nextX < 0 || nextX >= m || nextY < 0 || nextY >= n || visited[nextX][nextY] {
			cur = (cur + 1) % 4
		}
		x += direc[cur][0]
		y += direc[cur][1]
	}

	return ret
}

func spiralOrder1(matrix [][]int) []int {
	if len(matrix) == 0 || len(matrix[0]) == 0 {
		return nil
	}
	m, n := len(matrix), len(matrix[0])
	var (
		ret                   = make([]int, m*n)
		left, right, up, down = 0, n - 1, 0, m - 1
		cur                   = 0
	)

	for left <= right && up <= down {
		for i := left; i <= right; i++ {
			ret[cur] = matrix[up][i]
			cur++
		}
		for j := up + 1; j <= down; j++ {
			ret[cur] = matrix[j][right]
			cur++
		}
		if left < right && up < down {
			for i := right - 1; i >= left; i-- {
				ret[cur] = matrix[down][i]
				cur++
			}
			for j := down - 1; j > up; j-- {
				ret[cur] = matrix[j][left]
				cur++
			}
		}

		left++
		right--
		up++
		down--
	}

	return ret
}
```

### c++ 实现

```c++
#include <iostream>
#include <vector>

using namespace std;

vector<int> printMatrix(vector<vector<int> >& matrix)
{
	vector<int> res;
    if (matrix.size() < 1 || matrix[0].size() < 1)
        return res;
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
    int a[][5] = {
		{1, 2, 3},
        {4, 5, 6},
        {7, 8, 9},
	};
	vector<vector<int> > matrix(3, vector<int> (3, 0));
	for (int m = 0; m < matrix.size(); m++)
	{
		for (int n = 0; n < matrix[m].size(); n++)
		{
			matrix[m][n] = a[m][n];
		}
	}
    vector<int> res;
    res = printMatrix(matrix);
    vector<int>::iterator it;
	for (it = res.begin(); it != res.end(); it++)
		cout << *it << " ";
    cout << endl;
	return 0;
}
```
