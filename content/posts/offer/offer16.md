---
title: "剑指offer16——合并两个排序的链表"
date: 2019-03-06T19:20:03+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

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

ListNode* Merge(ListNode* pHead1, ListNode* pHead2)
{
	ListNode *res = NULL;
	if (pHead1 == NULL)
		return pHead2;
	if (pHead2 == NULL)
		return pHead1;
	if (pHead1->val < pHead2->val)
	{
		res = pHead1;
		res->next = Merge(pHead1->next, pHead2);
	}
	else
	{
		res = pHead2;
		res->next = Merge(pHead1, pHead2->next);
	}
	return res;
}

int main()
{
	ios::sync_with_stdio(false);
	int n1, n2;
	ListNode *L = new ListNode;
	ListNode *L1 = new ListNode;
	ListNode *L2 = new ListNode;
	L->next = NULL;
	L1->next = NULL;
	L2->next = NULL;
	ListNode *q1 = L1;
	ListNode *q2 = L2;
	cin >> n1 >> n2;
	for (int i = 0; i < n1; i++)
	{
		ListNode *p = new ListNode;
		cin >> p->val;
		q1->next = p;
		q1 = p;
	}
	q1->next = NULL;
	for (int i = 0; i < n2; i++)
	{
		ListNode *p = new ListNode;
		cin >> p->val;
		q2->next = p;
		q2 = p;
	}
	q2->next = NULL;
	L = Merge(L1->next, L2->next);
	while (L != NULL)
	{
		cout << L->val << " ";
		L = L->next;
	}
	cout << endl;
	return 0;
}
```
