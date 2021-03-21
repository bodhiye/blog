---
title: "剑指offer03——数组中重复的数字"
date: 2021-03-21T16:52:00+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

　　在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

示例 1：

```bash
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```

限制：

2 <= n <= 100000

### 题解

　　首先拿到这道题最先想到的是用 map 处理，遍历整个数组，当某个数字在 map 中的 value 为 true 时，表示之前已经出现过这个数字。

　　但是如果在面试时面试官要求空间复杂度为 O(1) 时，就不能用额外的标记数组或者 map。对于这种数组元素在 [0, n-1] 范围内的问题，我们可以通过原地置换法把将值为 i 的数置换到下标为 i 的位置。如果下标 i 之前已经有对应值为 i 的数字，就说明数字 i 重复。

　　用题目中给的例子来模拟该过程：

```bash
0 1 2 3 4 5 6 下标
2 3 1 0 2 5 3 初始值
1 3 2 0 2 5 3 下标0的2和下标2的1置换
3 1 2 0 2 5 3 下标0的1和下标1的3置换
0 1 2 3 2 5 3 下标0的3和下标3的0置换
0 1 2 3 2 5 3 下标2的值已经为2，下标4上的2不能与其置换，故2为重复数字
```

### 源码

```go
package main

import "fmt"

func main() {
	var nums = []int{2, 3, 1, 0, 2, 5, 3}
	fmt.Println(findRepeatNumber(nums))
	fmt.Println(findRepeatNumber2(nums))
}

func findRepeatNumber(nums []int) int {
	var m = make(map[int]bool, len(nums))
	for _, num := range nums {
		if m[num] {
			return num
		}
		m[num] = true
	}
	return 0
}

// 原地置换法
func findRepeatNumber2(nums []int) int {
	for i, num := range nums {
		for nums[i] != i {
			if nums[i] == num {
				return nums[i]
			}
			nums[i], num = num, nums[i]
		}
	}
	return 0
}
```

```c++
#include <iostream>
#include <vector>

using namespace std; 

bool duplicate(int numbers[], int length, int *duplication) {

    vector<bool> b = {0};
    for (int i = 0; i < length; i++) {
        if (b[numbers[i]]) {
            *duplication = numbers[i];
            return true;
        }
        b[numbers[i]] = true;
    }
    return false;

}

int main() {

    ios::sync_with_stdio(false);
    int n, res;
    int a[1001];
    cin >> n;
    for (int i = 0; i < n; i++)
        cin >> a[i];
    cout << duplicate(a, n, &res) << endl;
    cout << res;
    return 0;

}
```
