---
title: "剑指offer10-I-斐波那契数列"
date: 2021-07-20T16:40:00+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

## 题目描述

写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项（即 F(N)）。斐波那契数列的定义如下：

```html
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
```

斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

## 示例

输入：n = 2
输出：1

输入：n = 5
输出：5

## 限制

`0 <= n <= 100`

## 题解

　　这道题目应该是面试中常考的算法题了，基本上大家都能想到解法，但是每个人能想到的解法不尽相同。斐波那契数列区题型区分度高，且马甲题众多，面试官偏爱这种题目，所以大家尽量掌握多种解法，才能在面试时从容应对。
　　首先能想到的应该是递归解法了，简单易懂，但是递归算法实际上重复计算了大量的数值，导致效率十分低下，时间复杂度达到了 O(2^N)，面试官肯定不愿意看到这种解法，一般 OJ 上这种解法肯定会超时。
　　当然也可以把递归时计算的数值保存下来，避免重复计算，这就是记忆化递归法，时间复杂度为 O(N)。
　　这道题很容易想到转移方程 f(n+1)=f(n)+f(n−1)，故可以使用动态规划来解，由于第 n 项只与 n-1 和 n-2 项有关系，故可以只存前两项的值，空间复杂度优化到 O(1)。
　　很多人觉得动态规划应该是最优解了吧，但其实除了通项式外最优解应该是`矩阵快速幂`解法，一般面试时不推荐给出通项式解法，毕竟证明过程就特别长，且容易给面试官留下背题的嫌疑，当然打表法也不推荐面试使用，在给出特定范围时为了过 OJ 打表法可以拿到最优解。下面给出矩阵运算的解法：
![fib](/images/offer/fib.png)
　　很容易看出来下面矩阵的 (n-1) 次阶乘和初始矩阵的乘积为第 n 项的值。
![matrix](/images/offer/matrix.png)
　　注意求矩阵阶乘时可以用到快速幂解法，通过奇偶分治法可以把时间复杂度降到 O(lgN)，这也是为什么用矩阵解法的原因。

## 源码

### golang 实现

```go
package main

import (
	"fmt"
)

// 递归
var dp [101]int

func fib(n int) int {
	if n < 2 {
		return n
	}
	if dp[n] > 0 {
		return dp[n]
	}
	dp[n] = fib(n-1) + fib(n-2)
	return dp[n] % 1000000007
}

// 动态规划
func fib1(n int) int {
	a, b := 0, 1
	for i := 0; i < n; i++ {
		a, b = b, (a+b)%1000000007
	}
	return a
}

// 矩阵快速幂
func fib2(n int) int {
	if n < 2 {
		return n
	}

	first := [][2]int{{2, 1}, {1, 0}}
	m := [][2]int{{1, 1}, {1, 0}}
	res := matrixPow(m, n-1)
	return matrixMul(first, res)[1][1]
}

func matrixPow(x [][2]int, n int) [][2]int {
	res := x
	for n != 0 {
		if n&1 == 1 { // 奇偶分治
			res = matrixMul(res, x)
		}
		x = matrixMul(x, x)
		n >>= 1
	}
	return res
}

func matrixMul(x, y [][2]int) [][2]int {
	m := make([][2]int, 2)
	m[0][0] = (x[0][0]*y[0][0] + x[0][1]*y[1][0]) % 1000000007
	m[0][1] = (x[0][0]*y[0][1] + x[0][1]*y[1][1]) % 1000000007
	m[1][0] = (x[1][0]*y[0][0] + x[1][1]*y[1][0]) % 1000000007
	m[1][1] = (x[1][0]*y[0][1] + x[1][1]*y[1][1]) % 1000000007
	return m
}

func main() {
	fmt.Println(fib(100))
	fmt.Println(fib1(100))
	fmt.Println(fib2(100))
}
```

### c++ 实现

```c++
#include <iostream>

using namespace std;

int dp[101];

int fib(int n)
{
	if (n == 0 || n == 1)return n;
	if (dp[n])return dp[n];
	else
		return dp[n] = fib(n - 1) + fib(n - 2);
}

int main()
{
	ios::sync_with_stdio(false);
	cout << fib(100) << endl;
	return 0;
}
```
