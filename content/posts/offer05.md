---
title: "用两个栈实现队列"
date: 2019-03-06T19:19:18+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

#### 题解

```c++
#include <iostream>
#include <stack>
#include <queue>

using namespace std;

stack<int> stack1, stack2;
queue<int> queue1, queue2;


void push1(int node)
{
	stack1.push(node);
}

int pop1()
{
	int node;
	if (stack2.empty())
	{
		while (!stack1.empty())
		{
			node = stack1.top();
			stack2.push(node);
			stack1.pop();
		}
	}
	node = stack2.top();
	stack2.pop();
	return node;
}

void push2(int node)
{
	queue1.push(node);
}

int pop2()
{
	int node;
	while (queue1.size() > 1)
	{
		int temp = queue1.front();
		queue1.pop();
		queue2.push(temp);
	}
	node = queue1.front();
	queue1.pop();
	while (queue2.size())
	{
		int temp = queue2.front();
		queue2.pop();
		queue1.push(temp);
	}
	return node;
}

int main()
{
	ios::sync_with_stdio(false);
	int n, temp;
	cin >> n;
	cout << "用两个栈实现一个队列：" << endl;
	for (int i = 0; i < n; i++)
	{
		cin >> temp;
		push1(temp);
	}
	while (!stack1.empty() || !stack2.empty())
	{
		cout << pop1() << " ";
	}
	cout << endl << "用两个队列实现一个栈：" << endl;
	for (int i = 0; i < n; i++)
	{
		cin >> temp;
		push2(temp);
	}
	while (!queue1.empty())
	{
		cout << pop2() << " ";
	}
	cout << endl;
	return 0;
}
```