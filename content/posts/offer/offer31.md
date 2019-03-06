---
title: "整数中1出现的次数（从1到n整数中1出现的次数）"
date: 2019-03-06T19:20:59+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

求出1~13的整数中1出现的次数,并算出100~1300的整数中1出现的次数？为此他特别数了一下1~13中包含1的数字有1、10、11、12、13因此共出现6次,但是对于后面问题他就没辙了。ACMer希望你们帮帮他,并把问题更加普遍化,可以很快的求出任意非负整数区间中1出现的次数（从1 到 n 中1出现的次数）。

#### 题解

```c++
#include <iostream>

using namespace std;

int NumberOf1Between1AndN_Solution(int n)
{
	if (n < 1)return 0;
	int count = 0, base = 1, round = n;
	while (round)
	{
		int i = round % 10;
		round /= 10;
		count += round * base;
		if (i == 1)
			count += (n % base + 1);
		else if (i > 1)
			count += base;
		base *= 10;
	}
	return count;
}

int main()
{
	ios::sync_with_stdio(false);
	int n;
	cin >> n;
	cout << NumberOf1Between1AndN_Solution(n) << endl;
	return 0;
}
```