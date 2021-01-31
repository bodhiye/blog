---
title: "剑指offer66——机器人的运动范围"
date: 2019-03-06T19:23:25+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

地上有一个m行和n列的方格。一个机器人从坐标0,0的格子开始移动，每一次只能向左，右，上，下四个方向移动一格，但是不能进入行坐标和列坐标的数位之和大于k的格子。 例如，当k为18时，机器人能够进入方格（35,37），因为3+5+3+7 = 18。但是，它不能进入方格（35,38），因为3+5+3+8 = 19。请问该机器人能够达到多少个格子？

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

int getSum(int n) {
    int sum = 0;
    while (n) {
        sum += n % 10;
        n /= 10;
    }
    return sum;
}

int moving(int threshold, int i, int j, int rows, int cols, vector<vector<int> > &flag) {
    if (i < 0 || i >= rows || j < 0 || j >= cols || flag[i][j] == 1 || getSum(i) + getSum(j) > threshold)
        return 0;
    flag[i][j] = 1;
    return moving(threshold, i - 1, j, rows, cols, flag) + moving(threshold, i + 1, j, rows, cols, flag) +
           moving(threshold, i, j - 1, rows, cols, flag) + moving(threshold, i, j + 1, rows, cols, flag) + 1;
}

int movingCount(int threshold, int rows, int cols) {
    vector<vector<int> > flag(rows);
    for (int i = 0; i < rows; i++)
        flag[i].resize(cols, 0);
    return moving(threshold, 0, 0, rows, cols, flag);
}

int main() {
    ios::sync_with_stdio(false);
    int m, n, k;
    cin >> m >> n >> k;
    cout << movingCount(k, m, n);
    return 0;
}
```
