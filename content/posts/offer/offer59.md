---
title: "剑指offer59——按之字形顺序打印二叉树"
date: 2019-03-06T19:22:54+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

请实现一个函数按照之字形打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右至左的顺序打印，第三行按照从左到右的顺序打印，其他行以此类推。

#### 题解

```c++
#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>

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

vector<vector<int> > Print(TreeNode *pRoot) {
    vector<vector<int> > res;
    if (!pRoot)return res;
    queue<TreeNode *> q;
    q.push(pRoot);
    bool even = false;
    while (!q.empty()) {
        vector<int> v;
        int size=q.size();
        for (int i = 0; i < size; ++i) {
            TreeNode *tmp = q.front();
            q.pop();
            v.push_back(tmp->val);
            if (tmp->left)q.push(tmp->left);
            if (tmp->right)q.push(tmp->right);
        }
        if (even)
            reverse(v.begin(), v.end());
        even = !even;
        res.push_back(v);
    }
    return res;
}

int main() {
    ios::sync_with_stdio(false);
    TreeNode *root = NULL;
    root = newTree();
    vector<vector<int> > res;
    res = Print(root);
    for (auto it = res.begin(); it != res.end(); ++it) {
        for (auto i = (*it).begin(); i != (*it).end(); ++i)
            cout << *i << " ";
        cout << endl;
    }
    return 0;
}
```
