---
title: "从尾到头打印链表"
date: 2019-03-06T19:19:09+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入一个链表，按链表值从尾到头的顺序返回一个ArrayList。

#### 题解

```c++
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

vector<int> dev;
stack<int> s;

struct ListNode {
	int val;
	ListNode* next;
	ListNode(int x) :val(x), next(NULL) {}
	ListNode() {}
};

vector<int> printListFromTailToHead(ListNode* head)
{
	/*if (head != NULL) {
		if (head->next != NULL) {
			dev = printListFromTailToHead(head->next);
		}
		dev.push_back(head->val);
	}*/
	if (head != NULL)
	{
		s.push(head->val);
		while ((head = head->next) != NULL)
		{
			s.push(head->val);
		}
		while (!s.empty())
		{
			dev.push_back(s.top());
			s.pop();
		}
	}
	return dev;
}

int main()
{
	ios::sync_with_stdio(false);
	int n, flag = true;
	cin >> n;
	ListNode* head = new ListNode;
	ListNode* L = new ListNode;
	for (int i = 0; i < n; i++)
	{
		ListNode* p = new ListNode;
		cin >> p->val;
		if (flag)
		{
			head = p;
			flag = false;
		}
		p->next = L;
		L->next = p;
		L = p;
	}
	L->next = NULL;
	printListFromTailToHead(head);
	vector<int>::iterator it;
	for (it = dev.begin(); it != dev.end(); ++it)
		cout << *it << " ";
	cout << endl;
	return 0;
}
```