---
title: "二叉树展开为链表"
date: 2021-01-24T21:13:14+08:00
draft: false
categories: ["Leetcode题解"]
tags: ["Leetcode"]
---

---

## 题目描述

给定一个二叉树，原地将它展开为一个单链表。

### 示例

#### 给定二叉树

``` html


    1
   / \
  2   5
 / \   \
3   4   6
```

将其展开为:

``` html
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

## 题解

### 前序遍历

　　将二叉树进行前序遍历，获得各节点被访问到的顺序链表，遍历链表重组二叉树。

``` go
package main

type TreeNode struct {
	Val   int
	Left  *TreeNode
	Right *TreeNode
}

func flatten(root *TreeNode) {
	list := preorderTraversal(root)
	for i := 1; i < len(list); i++ {
		pre, cur := list[i-1], list[i]
		pre.Left, pre.Right = nil, cur
	}
}

func preorderTraversal(root *TreeNode) []*TreeNode {
	var list []*TreeNode
	if root != nil {
		list = append(list, root)
		list = append(list, preorderTraversal(root.Left)...)
		list = append(list, preorderTraversal(root.Right)...)
	}
	return list
}
```

`时间复杂度` O(n)
`空间复杂度` O(n)

### 前驱节点

　　对于当前节点，如果左子树不为空，寻找左子树最右边的节点，置为前驱节点，将当前节点的右节点赋给前驱节点右节点，并将当前节点左节点赋给当前节点右节点，且把当前节点左节点置为空，更新当前节点右节点为新的当前节点，直到处理完所有节点。

``` go
package main

type TreeNode struct {
	Val   int
	Left  *TreeNode
	Right *TreeNode
}

func flatten2(root *TreeNode) {
	cur := root
	for cur != nil {
		if cur.Left != nil {
			next := cur.Left
			pre := next
			for pre.Right != nil {
				pre = pre.Right
			}
			pre.Right = cur.Right
			cur.Left, cur.Right = nil, next
		}
		cur = cur.Right
	}
}
```

`时间复杂度` O(n)
`空间复杂度` O(1)
