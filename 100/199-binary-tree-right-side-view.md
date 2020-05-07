---
title: 二叉树右视图
author: Jachin Lin
pub_date: 2020-05-08
summary: 层次遍历，每一层只保留最后一个节点
difficulty: Medium
tags:
    - 二叉树
    - Medium
---

## 描述

[199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)

Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

Example:

```
Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```
## 思路

层次遍历，每一层只保留最后一个节点。层次遍历见 [二叉树层次遍历](./102-binary-tree-level-order-traversal.html)。

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
    def rightSideView(self, root: TreeNode) -> List[int]:
        if not root:
            return []
        result = []
        q = [root]
        q_tmp = []
        
        while q:
            this_level_last_node = None
            while q:
                node = q.pop(0)
                if node.left:
                    q_tmp.append(node.left)
                if node.right:
                    q_tmp.append(node.right)
                this_level_last_node = node
            result.append(this_level_last_node.val)
            q, q_tmp = q_tmp, q
            
        return result
```