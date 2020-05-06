---
title: 二叉树中序遍历
author: Jachin Lin
pub_date: 2020-05-06
summary: 递归，或者使用栈。
difficulty: Medium
tags:
    - 二叉树
    - 栈
    - Medium
---

## 描述

[94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

Given a binary tree, return the inorder traversal of its nodes' values.

## 思路

二叉树是典型的递归结构，使用递归可以轻易地做出解答。

解法二是使用栈，将未遍历的节点（子树）放入栈中。

## 解答

递归

```python
from typing import List

# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        if not root:
            return []
        return self.inorderTraversal(root.left) + [root.val] + self.inorderTraversal(root.right) 
```

栈

```python
from typing import List

# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        if not root:
            return []
        result = []
        stack = [root]
        while stack:
            node = stack.pop()
            if not node.left and not node.right:
                result.append(node.val)
            else:
                if node.right:
                    stack.append(node.right)
                left = node.left
                node.left = node.right = None
                stack.append(node)
                if left:
                    stack.append(left)
        return result
```