---
title: "剑指offer64——滑动窗口的最大值"
date: 2019-03-06T19:23:18+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

给定一个数组和滑动窗口的大小，找出所有滑动窗口里数值的最大值。例如，如果输入数组{2,3,4,2,6,2,5,1}及滑动窗口的大小3，那么一共存在6个滑动窗口，他们的最大值分别为{4,4,6,6,6,5}； 针对数组{2,3,4,2,6,2,5,1}的滑动窗口有以下6个： {[2,3,4],2,6,2,5,1}， {2,[3,4,2],6,2,5,1}， {2,3,[4,2,6],2,5,1}， {2,3,4,[2,6,2],5,1}， {2,3,4,2,[6,2,5],1}， {2,3,4,2,6,[2,5,1]}。

#### 题解

```c++
#include <iostream>
#include <vector>
#include <deque>

using namespace std;

vector<int> maxInWindows(const vector<int> &num, unsigned int size) {
    vector<int> v;
    deque<int> d;
    for (unsigned int i = 0; i < num.size(); ++i) {
        while (d.size() && num[d.back()] <= num[i])
            d.pop_back();
        if (d.size() && i - d.front() + 1 > size)
            d.pop_front();
        d.push_back(i);
        if (size && i + 1 >= size)
            v.push_back(num[d.front()]);
    }
    return v;
}

int main() {
    ios::sync_with_stdio(false);
    vector<int> v, res;
    int n, k, tmp;
    cin >> n >> k;
    for (int i = 0; i < n; i++) {
        cin >> tmp;
        v.push_back(tmp);
    }
    res = maxInWindows(v, k);
    for (auto it = res.begin(); it != res.end(); ++it)
        cout << *it << " ";
    return 0;
}
```
