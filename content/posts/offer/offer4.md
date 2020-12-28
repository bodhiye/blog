---
title: "重建二叉树"
date: 2019-03-06T19:19:14+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

struct TreeNode
{
	int val;
	TreeNode *left;
	TreeNode *right;
	TreeNode(int x) : val(x), left(NULL), right(NULL) {}
	TreeNode() {}
};

TreeNode* reConstructBinaryTree(vector<int> pre, vector<int> vin)
{
	int pre_len = pre.size();
	int vin_len = vin.size();
	if (pre_len == 0 || vin_len == 0 || pre_len != vin_len)
		return NULL;
	TreeNode *head = new TreeNode(pre[0]);//创建根节点
	int root_ind = 0;//记录root在中序中的下标
	for (int i = 0; i < vin_len; i++) {
		if (vin[i] == pre[0]) {
			root_ind = i;
			break;
		}
	}
	vector<int> vin_left, vin_right, pre_left, pre_right;
	for (int j = 0; j < root_ind; j++) {
		vin_left.push_back(vin[j]);
		pre_left.push_back(pre[j + 1]);//第一个为根根节点，跳过
	}
	for (int j = root_ind + 1; j < pre_len; j++) {
		vin_right.push_back(vin[j]);
		pre_right.push_back(pre[j]);
	}
	//递归
	head->left = reConstructBinaryTree(pre_left, vin_left);
	head->right = reConstructBinaryTree(pre_right, vin_right);
	return head;
}

void inorder(TreeNode* root)
{
	if (root)
	{
		inorder(root->left);
		cout << root->val << " ";
		inorder(root->right);
	}
}

int main()
{
	ios::sync_with_stdio(false);
	int pre[] = { 1,2,4,7,3,5,6,8 };
	int vin[] = { 4,7,2,1,5,3,8,6 };
	vector<int> pre_vec(pre, pre + 8);
	vector<int> vin_vec(vin, vin + 8);
	TreeNode *head;
	head = reConstructBinaryTree(pre_vec, vin_vec);
	inorder(head);
	cout << endl;
	return 0;
}
```