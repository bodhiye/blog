---
title: "剑指offer53——表示数值的字符串"
date: 2019-03-06T19:22:32+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100","5e2","-123","3.1416"和"-1E-16"都表示数值。 但是"12e","1a3.14","1.2.3","+-5"和"12e+4.3"都不是。

#### 题解

```c++
#include <iostream>
#include <string>

using namespace std;

bool isNumeric(char *string) {
    int n = strlen(string);
    if (n == 0 || (n == 1 && (string[0] < '0' || string[0] > '9')))
        return false;
    bool sign = false, dec = false, hasE = false;
    for (int i = 0; i < n; i++) {
        if (string[i] == '+' || string[i] == '-') {
            if (!sign && i > 0 && string[i - 1] != 'e' && string[i - 1] != 'E')
                return false;
            if (sign && string[i - 1] != 'e' && string[i - 1] != 'E')
                return false;
            sign = true;
        } else if (string[i] == 'e' || string[i] == 'E') {
            if (i == 0 || i == n - 1)
                return false;
            if (hasE)
                return false;
            hasE = true;
        } else if (string[i] == '.') {
            if (hasE || dec || i == 0 || i == n - 1)
                return false;
            dec = true;
        } else if (string[i] < '0' || string[i] > '9')
            return false;
    }
    return true;
}

int main() {
    ios::sync_with_stdio(false);
    char a[101];
    cin >> a;
    cout << isNumeric(a);
    return 0;
}
```
