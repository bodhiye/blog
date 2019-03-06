---
title: "二叉树的镜像"
date: 2019-03-06T19:20:12+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

操作给定的二叉树，将其变换为源二叉树的镜像。

#### 输入描述:

二叉树的镜像定义：源二叉树 
    	    8
    	   /  \
    	  6   10
    	 / \  / \
    	5  7 9 11
    	镜像二叉树
    	    8
    	   /  \
    	  10   6
    	 / \  / \
        11 9 7  5

#### 题解

```c++
#include <iostream>

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

void preOrder(TreeNode *pRoot)
{
	if (pRoot)
	{
		cout << pRoot->val << " ";
		preOrder(pRoot->left);
		preOrder(pRoot->right);
	}
}

void Mirror(TreeNode *pRoot)
{
	if (pRoot == NULL)
		return;
	TreeNode *temp = pRoot->left;
	pRoot->left = pRoot->right;
	pRoot->right = temp;
	Mirror(pRoot->left);
	Mirror(pRoot->right);
}

int main()
{
	ios::sync_with_stdio(false);
	TreeNode* pRoot = NULL;
	pRoot = newTree();
	Mirror(pRoot);
	preOrder(pRoot);
	cout << endl;
	return 0;
}
```