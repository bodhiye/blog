---
title: "删除链表中重复的结点"
date: 2019-03-06T19:22:44+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->5

#### 题解

```c++
#include <iostream>

using namespace std;

struct ListNode {
    int val;
    ListNode *next;

    ListNode(int x) : val(x), next(NULL) {}

    ListNode() {}
};

ListNode *newList() {
    ListNode *L = new ListNode;
    L->next = NULL;
    ListNode *q = L;
    int n;
    cin >> n;
    for (int i = 0; i < n; i++) {
        ListNode *p = new ListNode;
        cin >> p->val;
        q->next = p;
        q = p;
    }
    q->next = NULL;
    return L->next;
}

void print(ListNode *pHead) {
    while (pHead) {
        cout << pHead->val << " ";
        pHead = pHead->next;
    }
}

ListNode *deleteDuplication(ListNode *pHead) {
    if (pHead == NULL || pHead->next == NULL)
        return pHead;
    if (pHead->val == pHead->next->val) {
        ListNode *pNode = pHead->next;
        while (pNode != NULL && pNode->val == pHead->val) {
            pNode = pNode->next;
        }
        return deleteDuplication(pNode);
    } else {
        pHead->next = deleteDuplication(pHead->next);
        return pHead;
    }
}

int main() {
    ios::sync_with_stdio(false);
    ListNode *L = newList();
    ListNode *res = deleteDuplication(L);
    print(res);
    return 0;
}
```