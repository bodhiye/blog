---
title: "二叉树的深度"
date: 2019-03-06T19:21:22+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入一棵二叉树，求该树的深度。从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。

#### 题解

```c++
#include <iostream>
#include <algorithm>

using namespace std;

struct TreeNode
{
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) : val(x), left(NULL), right(NULL) {}
	TreeNode() {}
};

TreeNode* newTree()
{
	TreeNode* node = new TreeNode;
	int x;
	cin >> x;
	if (!x)node = NULL;
	else
	{
		node->val = x;
		node->left = newTree();
		node->right = newTree();
	}
	return node;
}

int TreeDepth(TreeNode* root)
{
	if (!root)return 0;
	return max(TreeDepth(root->left) + 1, TreeDepth(root->right) + 1);
}

int main()
{
	ios::sync_with_stdio(false);
	TreeNode* root = NULL;
	root = newTree();
	cout << TreeDepth(root) << endl;
	return 0;
}
```