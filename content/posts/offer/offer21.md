---
title: "栈的压入、弹出序列"
date: 2019-03-06T19:20:24+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

#### 题解

```c++
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

bool IsPopOrder(vector<int> pushV, vector<int> popV)
{
	stack<int> s;
	for (int i = 0, j = 0; i < pushV.size(); i++)
	{
		s.push(pushV[i]);
		while (!s.empty() && s.top() == popV[j])
		{
			s.pop();
			j++;
		}
	}
	return s.empty();
}

int main()
{
	ios::sync_with_stdio(false);
	vector<int> pushV, popV;
	int n, temp;
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		cin >> temp;
		pushV.push_back(temp);
	}
	for (int i = 0; i < n; i++)
	{
		cin >> temp;
		popV.push_back(temp);
	}
	cout << IsPopOrder(pushV, popV) << endl;
	return 0;
}
```