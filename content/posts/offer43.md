---
title: "左旋转字符串"
date: 2019-03-06T19:21:52+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

汇编语言中有一种移位指令叫做循环左移（ROL），现在有个简单的任务，就是用字符串模拟这个指令的运算结果。对于一个给定的字符序列S，请你把其循环左移K位后的序列输出。例如，字符序列S=”abcXYZdef”,要求输出循环左移3位后的结果，即“XYZdefabc”。是不是很简单？OK，搞定它！

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

string LeftRotateString(string str, int n) {
    int len = str.length();
    str += str;
    if (len == 0)
        return "";
    n = n % len;
    return str.substr(n, len);
}

int main() {
    ios::sync_with_stdio(false);
    string s;
    cin >> s;
    int n;
    cin >> n;
    cout << LeftRotateString(s, n);
    return 0;
}
```