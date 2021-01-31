---
title: "剑指offer62——二叉搜索树的第k个结点"
date: 2019-03-06T19:23:07+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

给定一棵二叉搜索树，请找出其中的第k小的结点。例如， （5，3，7，2，4，6，8）    中，按结点数值大小顺序第三小结点的值为4。

#### 题解

```c++
#include <iostream>
#include <string>

using namespace std;

struct TreeNode {
    int val;
    struct TreeNode *left;
    struct TreeNode *right;

    TreeNode(int x) :
            val(x), left(NULL), right(NULL) {
    }

    TreeNode() {}
};

TreeNode *newTree() {
    TreeNode *node = new TreeNode;
    int x;
    cin >> x;
    if (!x)node = NULL;
    else {
        node->val = x;
        node->left = newTree();
        node->right = newTree();
    }
    return node;
}

int count = 0;

TreeNode *KthNode(TreeNode *pRoot, int k) {
    if (pRoot) {
        TreeNode *node = KthNode(pRoot->left, k);
        if (node) return node;
        if (++count == k)return pRoot;
        node = KthNode(pRoot->right, k);
        if (node)return node;
    }
    return NULL;
}

int main() {
    ios::sync_with_stdio(false);
    int k;
    cin >> k;
    TreeNode *root = NULL;
    root = newTree();
    cout << KthNode(root, k)->val;
    return 0;
}
```
