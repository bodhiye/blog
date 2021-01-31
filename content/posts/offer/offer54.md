---
title: "剑指offer54——字符流中第一个不重复的字符"
date: 2019-03-06T19:22:36+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符"go"时，第一个只出现一次的字符是"g"。当从该字符流中读出前六个字符“google"时，第一个只出现一次的字符是"l"。

#### 输出描述

如果当前字符流没有存在出现一次的字符，返回#字符。

#### 题解

```c++
#include <iostream>
#include <map>
#include <vector>

using namespace std;

map<char, int> m;
vector<int> v;

void Insert(char ch) {
    v.push_back(ch);
    m[ch]++;
}

char FirstAppearingOnce() {
    for (auto it = v.begin(); it != v.end(); ++it)
        if (m[*it] == 1)
            return *it;
    return '#';
}

int main() {
    ios::sync_with_stdio(false);
    char c;
    int n;
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> c;
        Insert(c);
    }
    cout << FirstAppearingOnce();
    return 0;
}
```
