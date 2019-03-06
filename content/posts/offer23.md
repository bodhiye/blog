---
title: "二叉搜索树的后序遍历序列"
date: 2019-03-06T19:20:31+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出Yes,否则输出No。假设输入的数组的任意两个数字都互不相同。

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

//bool VerifySquenceOfBST(vector<int> sequence)
//{
//	int len = sequence.size();
//	if (!len)return false;
//	while (--len)
//	{
//		int i = 0;
//		while (sequence[i++] < sequence[len]);
//		while (sequence[i++] > sequence[len]);
//		if (i < len)return false;
//	}
//	return true;
//}

bool judge(vector<int>& v, int l, int r)
{
	if (l >= r)return true;
	int i = r;
	while (i > l&&v[--i] > v[r]);
	for (int j = i - 1; j >= l; j--)
		if (v[j] > v[r])return false;
	return judge(v, l, i - 1) && judge(v, i, r - 1);
}

bool VerifySquenceOfBST(vector<int> sequence)
{
	int len = sequence.size();
	if (!len)return false;
	return judge(sequence, 0, len - 1);
}

int main()
{
	ios::sync_with_stdio(false);
	vector<int> v;
	int n, temp;
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		cin >> temp;
		v.push_back(temp);
	}
	cout << VerifySquenceOfBST(v) << endl;
	return 0;
}
```