---
title: "剑指offer09-用两个栈实现队列"
date: 2021-06-07T00:19:00+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

## 题目描述

　　用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

## 示例

示例 1：

输入：
`["CQueue","appendTail","deleteHead","deleteHead"]`
`[[],[3],[],[]]`
输出：
`[null,null,3,-1]`

示例 2：

输入：
`["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]`
`[[],[],[5],[2],[],[]]`
输出：
`[null,-1,null,null,5,2]`

## 限制

- 1 <= values <= 10000
- 最多会对 appendTail、deleteHead 进行 10000 次调用

## 题解

　　本题利用两个栈模拟一个队列，第一个栈实现插入操作，第二个栈实现删除操作。
　　栈的特点是先入后出，而队列是先进先出。利用第二个栈来保存第一个栈当前所有的元素，依次 pop 出要删除的元素，直到第二个栈为空。当第二个栈为空则又依次把第一个栈的所有元素 push 进栈。
　　下面是模拟过程
　　push stack1　3   stack2
                2
                1
   pop  stack1      stack2  ~~1~~
　　　　　　　　　　　　　　　　　　2
                              3
　　push stack1　4   stack2    2
                              3
   pop  stack1  4   stack2  ~~2~~
                              3

## 源码

### golang 实现

```go
package main

import "container/list"

type CQueue struct {
	stack1 *list.List
	stack2 *list.List
}

func Constructor() CQueue {
	return CQueue{
		stack1: list.New(),
		stack2: list.New(),
	}
}

func (this *CQueue) AppendTail(value int) {
	this.stack1.PushBack(value)
}

func (this *CQueue) DeleteHead() int {
	if this.stack2.Len() == 0 {
		for this.stack1.Len() > 0 {
			this.stack2.PushBack(this.stack1.Remove(this.stack1.Back()))
		}
	}
	if this.stack2.Len() != 0 {
		e := this.stack2.Back()
		this.stack2.Remove(e)
		return e.Value.(int)
	}
	return -1
}
```

### c++ 实现

```c++
#include <iostream>
#include <stack>
#include <queue>

using namespace std;

// 两个栈模拟一个队列
class CQueue {
    stack<int> stack1, stack2;
public:
    CQueue() {
        while (!stack1.empty()) {
            stack1.pop();
        }
        while (!stack2.empty()) {
            stack2.pop();
        }
    }
    
    void appendTail(int value) {
        stack1.push(value);
    }
    
    int deleteHead() {
        if (stack2.empty()) {
            while (!stack1.empty()) {
                stack2.push(stack1.top());
                stack1.pop();
            }
        } 
        if (stack2.empty()) {
            return -1;
        } else {
            int deleteItem = stack2.top();
            stack2.pop();
            return deleteItem;
        }
    }
};

// 两个队列模拟一个栈
class CStack {
    queue<int> queue1, queue2;
public:
    CStack() {
        while (!queue1.empty()) {
            queue1.pop();
        }
        while (!queue2.empty()) {
            queue2.pop();
        }
    }
    
    void push(int value) {
        queue1.push(value);
    }
    
    int pop() {
        int node;
        while (queue1.size() > 1)
        {
            queue2.push(queue1.front());
            queue1.pop();
        }
        node = queue1.front();
        queue1.pop();
        while (queue2.size())
        {
            queue1.push(queue2.front());
            queue2.pop();
        }
        return node;
    }
};
```
