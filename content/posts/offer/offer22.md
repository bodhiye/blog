---
title: "剑指offer22——从上往下打印二叉树"
date: 2019-03-06T19:20:28+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

从上往下打印出二叉树的每个节点，同层节点从左至右打印。

#### 题解

```c++
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

struct TreeNode
{
	int val;
	TreeNode *left;
	TreeNode *right;
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

vector<int> PrintFromTopToBottom(TreeNode* root)
{
	queue<TreeNode*> q;
	q.push(root);
	vector<int> v;
	if (!root)
		return v;
	while (!q.empty())
	{
		root = q.front();
		q.pop();
		v.push_back(root->val);
		if (root->left)q.push(root->left);
		if (root->right)q.push(root->right);
	}
	return v;
}

int main()
{
	ios::sync_with_stdio(false);
	vector<int> res;
	TreeNode* root = NULL;
	root = newTree();
	res = PrintFromTopToBottom(root);
	vector<int>::iterator it;
	for (it = res.begin(); it != res.end(); it++)
		cout << *it << " ";
	cout << endl;
	return 0;
}
```
