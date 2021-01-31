---
title: "剑指offer6——旋转数组的最小数字"
date: 2019-03-06T19:19:22+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。 输入一个非减排序的数组的一个旋转，输出旋转数组的最小元素。 例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。 NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

#### 题解

```c++
#include <iostream>
#include <vector>

using namespace std;

int minNumberInRotateArray(vector<int> rotateArray)
{
	int len = rotateArray.size();
	if (!len)
		return 0;
	int low = 0, high = len - 1;
	while (low < high)
	{
		int mid = low + ((high - low) >> 1);
		if (rotateArray[mid] > rotateArray[high])
			low = mid + 1;
		else if (rotateArray[mid] < rotateArray[high])
			high = mid;
		else
			high--;
	}
	return rotateArray[low];
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
	cout << minNumberInRotateArray(v) << endl;
	return 0;
}
```
