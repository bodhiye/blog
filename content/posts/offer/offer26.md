---
title: "剑指offer26——二叉搜索树与双向链表"
date: 2019-03-06T19:20:41+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

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

TreeNode* leftHead = NULL;
TreeNode* rightHead = NULL;

TreeNode* Convert(TreeNode* pRootOfTree)
{
	if (pRootOfTree == NULL) return NULL;
	Convert(pRootOfTree->left);
	if (rightHead == NULL)
		leftHead = rightHead = pRootOfTree;
	else
	{
		rightHead->right = pRootOfTree;
		pRootOfTree->left = rightHead;
		rightHead = pRootOfTree;
	}
	Convert(pRootOfTree->right);
	return leftHead;
}

void print(TreeNode* node)
{
	while (node)
	{
		cout << node->val << " ";
		node = node->right;
	}
	cout << endl;
}

int main()
{
	ios::sync_with_stdio(false);
	TreeNode* pRoot = NULL;
	pRoot = newTree();
	print(Convert(pRoot));
	return 0;
}
```
