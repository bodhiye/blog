---
title: "剑指offer32——把数组排成最小的数"
date: 2019-03-06T19:21:03+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。例如输入数组{3，32，321}，则打印出这三个数字能排成的最小数字为321323。

#### 题解

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

static bool cmp(int &a, int &b)
{
	string aa = to_string(a);
	string bb = to_string(b);
	return (aa + bb) < (bb + aa);
}

string PrintMinNumber(vector<int> numbers)
{
	string res;
	sort(numbers.begin(), numbers.end(), cmp);
	vector<int>::iterator it;
	for (it = numbers.begin(); it != numbers.end(); it++)
	{
		int temp = *it;
		res += to_string(temp);
	}
	return res;
}

int main()
{
	ios::sync_with_stdio(false);
	vector<int> v;
	int n;
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		int temp;
		cin >> temp;
		v.push_back(temp);
	}
	cout << PrintMinNumber(v) << endl;
	return 0;
}
```
