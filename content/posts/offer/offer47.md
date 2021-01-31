---
title: "剑指offer47——求1+2+3+...+n"
date: 2019-03-06T19:22:07+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

求1+2+3+...+n，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

#### 题解

```c++
#include <iostream>

using namespace std;

int Sum_Solution(int n) {
    int res = n;
    res && (res += Sum_Solution(n - 1));
    return res;
}

int Sum_Solution1(int n) {
    bool a[n][n + 1];
    return sizeof(a) >> 1;
}

int main() {
    ios::sync_with_stdio(false);
    int n;
    cin >> n;
    cout << Sum_Solution(n) << endl;
    cout << Sum_Solution1(n);
    return 0;
}
```
