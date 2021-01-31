---
title: "剑指offer25——复杂链表的复制"
date: 2019-03-06T19:20:38+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针指向任意一个节点），返回结果为复制后复杂链表的head。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）

#### 题解

```c++
#include <iostream>

using namespace std;

struct RandomListNode
{
	int label;
	RandomListNode *next, *random;
	RandomListNode(int x) : label(x), next(NULL), random(NULL) {}
	RandomListNode() {}
};

RandomListNode* newList()
{
	RandomListNode* L = new RandomListNode;
	L->next = NULL;
	L->random = NULL;
	RandomListNode* q = L;
	int n;
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		RandomListNode *p = new RandomListNode;
		cin >> p->label;
		q->next = p;
		q->random = p;
		q = p;
	}
	q->next = NULL;
	q->random = NULL;
	return L->next;
}

RandomListNode* Clone(RandomListNode* pHead)
{
	if (!pHead) return NULL;
	RandomListNode* currNode = pHead;
	while (currNode)
	{
		RandomListNode* node = new RandomListNode(currNode->label);
		node->next = currNode->next;
		currNode->next = node;
		currNode = node->next;
	}
	currNode = pHead;
	while (currNode)
	{
		RandomListNode* node = currNode->next;
		if (currNode->random)
			node->random = currNode->random->next;
		currNode = node->next;
	}
	RandomListNode* pCloneHead = pHead->next;
	RandomListNode* tmp;
	currNode = pHead;
	while (currNode->next)
	{
		tmp = currNode->next;
		currNode->next = tmp->next;
		currNode = tmp;
	}
	return pCloneHead;
}

int main()
{
	ios::sync_with_stdio(false);
	RandomListNode* L1 = newList();
	RandomListNode* L2 = Clone(L1);
	RandomListNode* p = L2;
	while (p)
	{
		cout << p->label << " ";
		p = p->next;
	}
	cout << endl;
	return 0;
}
```
