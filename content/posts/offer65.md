---
title: "矩阵中的路径"
date: 2019-03-06T19:23:21+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一个格子开始，每一步可以在矩阵中向左，向右，向上，向下移动一个格子。如果一条路径经过了矩阵中的某一个格子，则之后不能再次进入这个格子。 例如 a b c e s f c s a d e e 这样的3 X 4 矩阵中包含一条字符串"bcced"的路径，但是矩阵中不包含"abcb"路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入该格子。

#### 题解

```c++
#include <iostream>
#include <string>
#include <vector>

using namespace std;

bool path(char *matrix, int rows, int cols, int i, int j, char *str, int k, vector<bool> flag) {
    int index = i * cols + j;
    if (i < 0 || i >= rows || j < 0 || j >= cols || matrix[index] != str[k] || flag[index])
        return false;
    if (k == strlen(str) - 1)
        return true;
    flag[index] = true;
    if (path(matrix, rows, cols, i - 1, j, str, k + 1, flag) || path(matrix, rows, cols, i + 1, j, str, k + 1, flag) ||
        path(matrix, rows, cols, i, j - 1, str, k + 1, flag) || path(matrix, rows, cols, i, j + 1, str, k + 1, flag))
        return true;
    flag[index] = false;
    return false;
}

bool hasPath(char *matrix, int rows, int cols, char *str) {
    vector<bool> flag(rows * cols, false);
    for (int i = 0; i < rows; i++)
        for (int j = 0; j < cols; j++)
            if (path(matrix, rows, cols, i, j, str, 0, flag))
                return true;
    return false;
}

int main() {
    ios::sync_with_stdio(false);
    int rows, cols;
    char s[101], str[101];
    cin >> rows >> cols >> s >> str;
    cout << hasPath(s, rows, cols, str);
    return 0;
}
```