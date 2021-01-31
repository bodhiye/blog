---
title: "剑指offer49——把字符串转换成整数"
date: 2019-03-06T19:22:15+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

将一个字符串转换成一个整数(实现Integer.valueOf(string)的功能，但是string不符合数字要求时返回0)，要求不能使用字符串转换整数的库函数。 数值为0或者字符串不是一个合法的数值则返回0。

#### 输入描述

输入一个字符串,包括数字字母符号,可以为空

#### 输出描述

如果是合法的数值表达则返回该数字，否则返回0

#### 示例1

```html
输入

+2147483647
    1a33

输出

2147483647
    0
```

#### 题解

```c++
#include <iostream>

using namespace std;

int StrToInt(string str) {
    int len = str.length();
    int flag = 1;
    long long res = 0;
    if (!len)return 0;
    if (str[0] == '-')flag = -1;
    for (int i = (str[0] == '+' || str[0] == '-') ? 1 : 0; i < len; i++) {
        if (!(str[i] >= '0' && str[i] <= '9'))return 0;
        res = res * 10 + (str[i] - '0');
    }
    return res * flag;
}

int main() {
    ios::sync_with_stdio(false);
    string s;
    cin >> s;
    cout << StrToInt(s);
    return 0;
}
```
