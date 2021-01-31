---
title: "剑指offer55——链表中环的入口结点"
date: 2019-03-06T19:22:40+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

给一个链表，若其中包含环，请找出该链表的环的入口结点，否则，输出null。

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

ListNode *EntryNodeOfLoop(ListNode *pHead) {
    if (pHead == NULL || pHead->next == NULL)
        return NULL;
    ListNode *p1 = pHead, *p2 = pHead;
    while (p2 != NULL && p2->next != NULL) {
        p1 = p1->next;
        p2 = p2->next->next;
        if (p1 == p2) {
            p2 = pHead;
            while (p1 != p2) {
                p1 = p1->next;
                p2 = p2->next;
            }
            if (p1 == p2)
                return p1;
        }
    }
    return NULL;
}

int main() {
    ios::sync_with_stdio(false);
    ListNode *L = newList();
    cout << EntryNodeOfLoop(L)->val;
    return 0;
}
```
