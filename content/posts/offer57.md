---
title: "二叉树的下一个结点"
date: 2019-03-06T19:22:48+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

给定一个二叉树和其中的一个结点，请找出中序遍历顺序的下一个结点并且返回。注意，树中的结点不仅包含左右子结点，同时包含指向父结点的指针。

#### 题解

```c++
#include <iostream>

using namespace std;

struct TreeLinkNode {
    int val;
    struct TreeLinkNode *left;
    struct TreeLinkNode *right;
    struct TreeLinkNode *next;

    TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}

    TreeLinkNode() {}
};

TreeLinkNode *newTree() {
    TreeLinkNode *node = new TreeLinkNode;
    int x;
    cin >> x;
    if (!x)node = NULL;
    else {
        node->val = x;
        node->left->next = node;
        node->left = newTree();
        node->right->next = node;
        node->right = newTree();
    }
    return node;
}

TreeLinkNode *GetNext(TreeLinkNode *pNode) {
    if (!pNode)return NULL;
    if (pNode->right) {
        pNode = pNode->right;
        while (pNode->left)pNode = pNode->left;
        return pNode;
    }
    while (pNode->next) {
        if (pNode->next->left == pNode)
            return pNode->next;
        pNode = pNode->next;
    }
    return NULL;
}

int main() {
    ios::sync_with_stdio(false);
    TreeLinkNode *node = newTree();
    TreeLinkNode *pNode;
    TreeLinkNode *res = GetNext(pNode);
    cout << res->val;
    return 0;
}
```