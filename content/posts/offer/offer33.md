---
title: "剑指offer33——丑数"
date: 2019-03-06T19:21:06+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

把只包含质因子2、3和5的数称作丑数（Ugly Number）。例如6、8都是丑数，但14不是，因为它包含质因子7。 习惯上我们把1当做是第一个丑数。求按从小到大的顺序的第N个丑数。

#### 题解

```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int GetUglyNumber_Solution(int index)
{
	if (!index)return 0;
	vector<int> v(index);
	v[0] = 1;
	int t2 = 0, t3 = 0, t5 = 0;
	for (int i = 1; i < index; i++)
	{
		v[i] = min(v[t2] * 2, min(v[t3] * 3, v[t5] * 5));
		if (v[i] == v[t2] * 2)t2++;
		if (v[i] == v[t3] * 3)t3++;
		if (v[i] == v[t5] * 5)t5++;
	}
	return v[index - 1];
}

int main()
{
	ios::sync_with_stdio(false);
	int n;
	cin >> n;
	cout << GetUglyNumber_Solution(n) << endl;
	return 0;
}
```
