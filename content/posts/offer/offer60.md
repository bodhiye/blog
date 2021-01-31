---
title: "剑指offer60——把二叉树打印成多行"
date: 2019-03-06T19:23:00+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

从上到下按层打印二叉树，同一层结点从左至右输出。每一层输出一行。

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
