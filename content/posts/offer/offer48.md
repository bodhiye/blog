---
title: "剑指offer48——不用加减乘除做加法"
date: 2019-03-06T19:22:11+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

写一个函数，求两个整数之和，要求在函数体内不得使用+、-、*、/四则运算符号。

#### 题解

```c++
#include <iostream>

using namespace std;

int Add(int num1, int num2) {
    while (num2) {
        int carry = num1 ^num2;
        num2 = (num1 & num2) << 1;
        num1 = carry;
    }
    return num1;
}

int main() {
    ios::sync_with_stdio(false);
    int a, b;
    cin >> a >> b;
    cout << Add(a, b);
    return 0;
}
```
