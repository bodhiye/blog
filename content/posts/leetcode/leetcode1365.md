---
title: "有多少小于当前数字的数字"
date: 2020-12-28T23:13:14+08:00
draft: false
categories: ["Leetcode题解"]
tags: ["Leetcode"]
---

---

## 题目描述

给你一个数组 nums，对于其中每个元素 nums[i]，请你统计数组中比它小的所有数字的数目。
换而言之，对于每个 nums[i] 你必须计算出有效的 j 的数量，其中 j 满足 j != i 且 nums[j] < nums[i]。
以数组形式返回答案。

### 示例 1

``` html
输入：nums = [8,1,2,2,3]
输出：[4,0,1,1,3]
解释： 
对于 nums[0]=8 存在四个比它小的数字：（1，2，2 和 3）。 
对于 nums[1]=1 不存在比它小的数字。
对于 nums[2]=2 存在一个比它小的数字：（1）。 
对于 nums[3]=2 存在一个比它小的数字：（1）。 
对于 nums[4]=3 存在三个比它小的数字：（1，2 和 2）。
```

### 示例 2

``` html
输入：nums = [6,5,4,8]
输出：[2,1,0,3]
```

### 示例 3

``` html
输入：nums = [7,7,7,7]
输出：[0,0,0,0]
```

## 提示

- 2 <= nums.length <= 500
- 0 <= nums[i] <= 100

## 题解

``` go
package main

import (
	"fmt"
	"sort"
)

func main() {
	nums := [][]int{{8, 1, 2, 2, 3}, {6, 5, 4, 8}, {7, 7, 7, 7}}
	for _, data := range nums {
		fmt.Println(smallerNumbersThanCurrent(data))
	}
}

type pair struct {
	Pos   int
	Value int
}

// 快速排序
func smallerNumbersThanCurrent(nums []int) []int {
	p := make([]pair, len(nums))
	for i, num := range nums {
		p[i] = pair{i, num}
	}
	sort.Slice(p, func(i, j int) bool { return p[i].Value < p[j].Value })

	res := make([]int, len(nums))
	var small int
	for i := range p {
		if i > 0 && p[i].Value != p[i-1].Value {
			small = i
		}
		res[p[i].Pos] = small
	}

	return res
}

// 计数排序
func smallerNumbersThanCurrent1(nums []int) []int {
	cnt := [101]int{}
    for _, v := range nums {
        cnt[v]++
    }
    for i := 0; i < 100; i++ {
		cnt[i+1] += cnt[i]
	}

    res := make([]int, len(nums))
    for i, v := range nums {
        if v > 0 {
            res[i] = cnt[v-1]
        }
    }
    return res
}
```
