---
title: 二叉树 zigzag 遍历
author: Jachin Lin
pub_date: 2020-05-08
summary: 层次遍历，使用一个 flag 标识遍历行的遍历方向。　
difficulty: Medium
tags:
    - 二叉树
    - Medium
---

## 描述

[103. Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

Given a binary tree, return the zigzag level order traversal of its nodes' values. 
(ie, from left to right, then right to left for the next level and alternate between).

## 思路

层次遍历，思路见 [二叉树层次遍历](./102-binary-tree-level-order-traversal.html)，使用一个 flag 标识遍历行的遍历方向。

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
    def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:
            return []
        result = []
        q = [root]
        q_tmp = []
        left_to_right = True
        
        while q:
            this_level = []
            while q:
                node = q.pop(0)
                if node.left:
                    q_tmp.append(node.left)
                if node.right:
                    q_tmp.append(node.right)
                if left_to_right:
                    this_level.append(node.val)
                else:
                    this_level.insert(0, node.val)
            result.append(this_level)
            left_to_right = not left_to_right
            q, q_tmp = q_tmp, q
        
        return result
```