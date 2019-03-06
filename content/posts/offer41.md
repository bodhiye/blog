---
title: "和为S的连续正数序列"
date: 2019-03-06T19:21:39+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck!

#### 输出描述:

```html
输出所有和为S的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序
```

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

vector<vector<int> > FindContinuousSequence(int sum) {
    vector<vector<int> > res;
    int low = 1, high = 2;
    while (low < high) {
        int tempsum = ((low + high) * (high - low + 1) >> 1);
        if (tempsum == sum) {
            vector<int> temp;
            for (int i = low; i <= high; i++)
                temp.push_back(i);
            res.push_back(temp);
            low++;
        } else if (tempsum < sum)
            high++;
        else
            low++;
    }
    return res;
}

int main() {
    ios::sync_with_stdio(false);
    int sum;
    vector<vector<int> > res;
    vector<int> temp;
    cin >> sum;
    res = FindContinuousSequence(sum);
    vector<vector<int> >::iterator iter;
    vector<int>::iterator it;
    for (iter = res.begin(); iter != res.end(); iter++) {
        temp = *iter;
        for (it = temp.begin(); it != temp.end(); it++)
            cout << *it << " ";
        cout << endl;
    }
    return 0;
}
```