---
title: "和为S的两个数字"
date: 2019-03-06T19:21:43+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。

#### 输出描述:

对应每个测试案例，输出两个数，小的先输出。

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

vector<int> FindNumbersWithSum(vector<int> array, int sum) {
    int low = 0, high = array.size() - 1;
    vector<int> res;
    while (low < high) {
        if (array[low] + array[high] == sum) {
            res.push_back(array[low]);
            res.push_back(array[high]);
            return res;
        } else if (array[low] + array[high] < sum)
            low++;
        else high--;
    }
    return res;
}

int main() {
    ios::sync_with_stdio(false);
    int sum, n, temp;
    vector<int> v;
    vector<int> res;
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> temp;
        v.push_back(temp);
    }
    cin >> sum;
    res = FindNumbersWithSum(v, sum);
    cout << res[0] << " " << res[1];
    return 0;
}
```