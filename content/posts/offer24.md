---
title: "二叉树中和为某一值的路径"
date: 2019-03-06T19:20:35+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入一颗二叉树的跟节点和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。(注意: 在返回值的list中，数组长度大的数组靠前)

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

vector<vector<int> > res;
vector<int> trace;

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

void dfs(TreeNode* node, int surplus)
{
	trace.push_back(node->val);
	if (node->val == surplus && !node->left && !node->right)
		res.push_back(trace);
	if (node->left)dfs(node->left, surplus - node->val);
	if (node->right)dfs(node->right, surplus - node->val);
	trace.pop_back();
}

vector<vector<int> > FindPath(TreeNode* root, int expectNumber)
{
	if (root)dfs(root, expectNumber);
	return res;
}

int main()
{
	ios::sync_with_stdio(false);
	TreeNode* root = NULL;
	root = newTree();
	int n;
	cin >> n;
	vector<vector<int> > ans;
	vector<int> temp;
	ans = FindPath(root, n);
	vector<vector<int> >::iterator it;
	vector<int>::iterator ite;
	for (it = ans.begin(); it != ans.end(); it++)
	{
		temp = *it;
		for (ite = temp.begin(); ite != temp.end(); ite++)
			cout << *ite << " ";
		cout << endl;
	}
	cout << endl;
	return 0;
}
```