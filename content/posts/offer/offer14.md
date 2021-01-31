---
title: "剑指offer14——链表中倒数第k个结点"
date: 2019-03-06T19:19:57+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入一个链表，输出该链表中倒数第k个结点。

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

ListNode* FindKthToTail(ListNode* pListHead, unsigned int k)
{
	ListNode *p, *q;
	p = q = pListHead;
	int i = 0;
	for (; p != NULL; i++)
	{
		if (i >= k)
			q = q->next;
		p = p->next;
	}
	return i < k ? NULL : q;
}

int main()
{
	ios::sync_with_stdio(false);
	int n, k;
	ListNode* L = new ListNode;
	L->next = NULL;
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		ListNode *p = new ListNode;
		cin >> p->val;
		p->next = L->next;
		L->next = p;
	}
	cin >> k;
	cout << FindKthToTail(L, k)->val << endl;
	return 0;
}
```
