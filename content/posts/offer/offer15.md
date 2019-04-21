---
title: "反转链表"
date: 2019-03-06T19:20:00+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入一个链表，反转链表后，输出新链表的表头。

#### 题解

```c++
#include <iostream>

using namespace std;

struct ListNode
{
	int val;
	ListNode *next;
	ListNode(int x) :val(x), next(NULL) {}
	ListNode() {}
};

ListNode *ReverseList(ListNode *pHead)
{
	if (pHead == NULL)
		return NULL;
	ListNode *pre = NULL, *next = NULL;
	while (pHead != NULL)
	{
		next = pHead->next;
		pHead->next = pre;
		pre = pHead;
		pHead = next;
	}
	return pre;
}

int main()
{
	ios::sync_with_stdio(false);
	int n;
	ListNode *L = new ListNode;
	L->next = NULL;
	ListNode *q = L;
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		ListNode *p = new ListNode;
		cin >> p->val;
		q->next = p;
		q = p;
	}
	q->next = NULL;
	L = ReverseList(L);
	while (L->next != NULL)
	{
		cout << L->val << " ";
		L = L->next;
	}
	cout << endl;
	return 0;
}
```