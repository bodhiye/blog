---
title: "剑指offer63——数据流中的中位数"
date: 2019-03-06T19:23:13+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。我们使用Insert()方法读取数据流，使用GetMedian()方法获取当前读取数据的中位数。

#### 题解

```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> v;
int n;

void Insert(int num) {
    v.push_back(num);
    n = v.size();
    for (int i = n - 1; i > 0 && v[i] < v[i - 1]; --i)
        swap(v[i], v[i - 1]);
}

double GetMedian() {
    return (v[(n - 1) >> 1] + v[n >> 1]) / 2.0;
}

int main() {
    ios::sync_with_stdio(false);
    int m, tmp;
    cin >> m;
    for (int i = 0; i < m; i++) {
        cin >> tmp;
        Insert(tmp);
    }
    cout << GetMedian();
    return 0;
}
```
