---
title: "剑指offer30-包含min函数的栈"
date: 2021-06-15T23:20:00+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

## 题目描述

　　定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

## 示例

示例 1：

```html
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();   --> 返回 0.
minStack.min();   --> 返回 -2.
```

## 限制

- 各函数的调用总次数不超过 20000 次

## 题解

　　本题除了维护一个普通栈以为，还需要维护一个单调栈，用来返回最小值。
　　当我们向栈压入一个元素时，如果该数这个数小于或等于单调栈栈顶的元素时，则同时将这个元素压入单调栈，这样可以保证单调栈栈顶元素一定是整个栈的最小元素，当弹出元素时比较该元素和单调栈栈顶元素是否相等，如果相等则弹出。

## 源码

### golang 实现

```go
package main

import (
	"container/list"
)

type MinStack struct {
	stack    *list.List
	minStack *list.List
}

func Constructor() MinStack {
	return MinStack{
		stack:    list.New(),
		minStack: list.New(),
	}
}

func (this *MinStack) Push(x int) {
	this.stack.PushBack(x)
	if this.minStack.Len() == 0 || this.minStack.Back().Value.(int) >= x {
		this.minStack.PushBack(x)
	}
}

func (this *MinStack) Pop() {
	if this.stack.Back().Value.(int) == this.minStack.Back().Value.(int) {
		this.minStack.Remove(this.minStack.Back())
	}
	this.stack.Remove(this.stack.Back())
}

func (this *MinStack) Top() int {
	return this.stack.Back().Value.(int)
}

func (this *MinStack) Min() int {
	return this.minStack.Back().Value.(int)
}
```

### c++ 实现

```c++
#include <iostream>
#include <stack>

using namespace std;

class MinStack {
    stack<int> stack, minStack;
public:
    MinStack() {
        while (!stack.empty()) {
            stack.pop();
        }
        while (!minStack.empty()) {
            minStack.pop();
        }   
    }
    
    void push(int x) {
        stack.push(x);
        if (minStack.empty() || x <= minStack.top())
		    minStack.push(x);
    }
    
    void pop() {
        if (stack.top() == minStack.top())
		    minStack.pop();
        stack.pop();
    }
    
    int top() {
        return stack.top();
    }
    
    int min() {
        return minStack.top();
    }
};
```
