---
title: 二叉树层次遍历
author: Jachin Lin
pub_date: 2020-05-07
summary: 使用两个队列，一个队列存放当前层的节点，一个队列存放下一层的节点。
difficulty: Medium
tags:
    - 二叉树
    - 栈
    - Medium
---

## 描述

[102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

## 思路

使用两个队列，一个队列存放当前层的节点，一个队列存放下一层的节点。只使用一个队列也是可以的，不过队列元素需要改为 `(node, level)` 二元组。

## 解答

```python
from typing import List

# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:
            return []
        result = []
        q = [root]
        q_tmp = []
        while q:
            this_result = []
            while q:
                node = q.pop(0)
                this_result.append(node.val)
                if node.left:
                    q_tmp.append(node.left)
                if node.right:
                    q_tmp.append(node.right)
            result.append(this_result)
            q, q_tmp = q_tmp, q
        return result
```