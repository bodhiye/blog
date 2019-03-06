---
title: "字符串的排列"
date: 2019-03-06T19:20:44+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。

#### 输入描述:

输入一个字符串,长度不超过9(可能有字符重复),字符只包括大小写字母。

#### 题解

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<string> res;

void perm(string str, int begin)
{
	if (begin == str.length())
		res.push_back(str);
	else
	{
		for (int i = begin; i < str.length(); i++)
		{
			if (i != begin && str[i] == str[begin]) continue;
			swap(str[begin], str[i]);
			perm(str, begin + 1);
			swap(str[begin], str[i]);
		}
	}
}

vector<string> Permutation(string str)
{
	if (str.length() == 0) return res;
	perm(str, 0);
	sort(res.begin(), res.end());
	return res;
}

int main()
{
	ios::sync_with_stdio(false);
	string s;
	cin >> s;
	vector<string> v = Permutation(s);
	vector<string>::iterator it;
	for (it = v.begin(); it != v.end(); it++)
		cout << *it << endl;
	return 0;
}
```