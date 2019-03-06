---
title: "树的子结构"
date: 2019-03-06T19:20:08+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）

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

bool IsSubtree(TreeNode *pRoot1, TreeNode *pRoot2)
{
	if (pRoot2 == NULL)
		return true;
	if (pRoot1 == NULL)
		return false;
	if (pRoot1->val != pRoot2->val)
		return false;
	return IsSubtree(pRoot1->left, pRoot2->left) && IsSubtree(pRoot1->right, pRoot2->right);
}

bool HasSubtree(TreeNode* pRoot1, TreeNode* pRoot2)
{
	if (pRoot1 == NULL || pRoot2 == NULL)
		return false;
	return IsSubtree(pRoot1, pRoot2) || HasSubtree(pRoot1->left, pRoot2) || HasSubtree(pRoot1->right, pRoot2);
}

int main()
{
	ios::sync_with_stdio(false);
	TreeNode* pRoot1 = NULL;
	TreeNode* pRoot2 = NULL;
	pRoot1 = newTree();
	pRoot2 = newTree();
	cout << HasSubtree(pRoot1, pRoot2) << endl;
	return 0;
}
```