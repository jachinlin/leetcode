---
title: 二叉搜索树迭代器
author: Jachin Lin
pub_date: 2020-05-09
summary: 中序遍历
difficulty: Medium
tags:
    - 二叉搜索树
    - Medium
---

## 描述

[173. Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/)

Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

Calling next() will return the next smallest number in the BST.

Note:

- next() and hasNext() should run in average O(1) time and uses O(h) memory, where h is the height of the tree.
- You may assume that next() call will always be valid, that is, there will be at least a next smallest number in the BST when next() is called.

## 思路

中序遍历，可以先中序遍历，把结果存放起来，然后依次迭代。这样 next() 的时间复杂度是 O(1)， 可以满足；但是空间复杂度却是 O(n)，大于 O(h) = O(logn)。

所以，我们可以只保存部分遍历节点（到一个栈中），节点数不超过树高，然后边调用 next() 边遍历二叉树剩余部分。

这部分节点就是，二叉树「尚未遍历的每一层的最左节点」。

## 解答

```python
from typing import List

# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class BSTIterator:

    def __init__(self, root: TreeNode):
        self._stack = []
        self._travel(root)
        
    def _travel(self, node):
        while node:
            self._stack.append(node)
            node = node.left
            
    def next(self) -> int:
        """
        @return the next smallest number
        """
        node = self._stack.pop()
        res = node.val
        self._travel(node.right)
        return res
        

    def hasNext(self) -> bool:
        """
        @return whether we have a next smallest number
        """
        return bool(self._stack)
```