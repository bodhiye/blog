---
title: "包含min函数的栈"
date: 2019-03-06T19:20:20+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

#### 题解

```c++
#include <iostream>
#include <stack>

using namespace std;

stack<int> s, smin;

void push(int value)
{
	s.push(value);
	if (smin.empty() || value <= smin.top())
		smin.push(value);
}

void pop()
{
	if (s.top() == smin.top())
		smin.pop();
	s.pop();
}

int top()
{
	return s.top();
}

int min()
{
	return smin.top();
}

int main()
{
	ios::sync_with_stdio(false);
	int temp;
	while (1)
	{
		cin >> temp;
		if (!temp)
			break;
		push(temp);
	}
	cout << min() << endl;
	return 0;
}
```