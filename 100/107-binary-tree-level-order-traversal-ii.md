---
title: 二叉树层次遍历 II
author: Jachin Lin
pub_date: 2020-05-07
summary: 使用两个队列，一个队列存放当前层的节点，一个队列存放下一层的节点。
difficulty: Easy
tags:
    - 二叉树
    - 队列
    - Easy
---

## 描述

[107. Binary Tree Level Order Traversal II](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/)

Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).
## 思路

思路同 [二叉树层次遍历](./102-binary-tree-level-order-traversal.html)，最后结果反转下就可以了。

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
    def levelOrderBottom(self, root: TreeNode) -> List[List[int]]:
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
            result.insert(0, this_result)
            q, q_tmp = q_tmp, q
        return result
```