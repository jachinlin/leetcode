---
title: 找出二叉搜索树中重复次数最多的元素
author: Jachin Lin
pub_date: 2020-06-01
tags:
    - 中序遍历
    - Easy
    - Golang
difficulty: Easy
summary: 利用二叉搜索树中序遍历的有序性，
---

## 描述 

[501. Find Mode in Binary Search Tree](https://leetcode.com/problems/find-mode-in-binary-search-tree/)

Given a binary search tree (BST) with duplicates, find all the mode(s) (the most frequently occurred element) in the given BST.

## 思路

二叉搜索树的一个特点就是，它的中序遍历是有序的，这样我们就可以把二叉搜索树当作有序数组来对待。
对于一个有序数组，找出重复次数最多的元素，如果只有一个结果的话，方法很简单，只需要使用以下四个变量，然后从左到右遍历一遍数组，在遍历过程更新这四个变量：

- curCnt: 当前元素出现的次数
- preVal: 上一个元素
- maxVal: 已经遍历过的元素中出现次数最多的元素
- maxCnt: maxVal 出现的次数

遍历完成后，maxVal 就是重复次数最多的元素，macCnt 就是重复的次数。

如果有多个元素重复次数是一样的且大于其他元素的，要找出这些元素的话，只需要在上面的基础上，
把变量 maxVal 改为 maxValList，更新 maxValList 的逻辑需要做一些调整：

如果 curCnt == maxCnt，则把 preVal 加入到 maxValList，如果 curCnt > maxCnt，则清空 maxValList，再把 preVal 加入到 maxValList。

对于搜索二叉树，思路同有序数组，只需要把从左到右的数组遍历，改为中序的二叉树遍历。

## 解答


```golang

// Definition for a binary tree node.
type TreeNode struct {
    Val int
    Left *TreeNode
    Right *TreeNode
}


func inOrderTraversal(tree *TreeNode, visit func(node *TreeNode)) {
	if tree == nil {
		return
	}
	inOrderTraversal(tree.Left, visit)
	visit(tree)
	inOrderTraversal(tree.Right, visit)
}

func findMode(root *TreeNode) []int {
	ans := make([]int, 0)
	if root == nil {
		return ans
	}
	curCnt := 0
	preVal := 0
	maxCnt := 0

	visit := func(node *TreeNode) {
		if node.Val == preVal {
			curCnt++
		} else {
			if curCnt >= maxCnt {
				if curCnt > maxCnt {
					ans = ans[:0]
				}
				maxCnt = curCnt
				ans = append(ans, preVal)
			}
			curCnt = 1
            preVal = node.Val
		}
		
	}
	inOrderTraversal(root, visit)

	if curCnt >= maxCnt {
		if curCnt > maxCnt {
			ans = ans[:0]
		}
		ans = append(ans, preVal)
	}
	return ans
}
```

ans 即为 maxValList。


