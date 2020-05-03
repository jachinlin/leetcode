---
title: 复制带有随机指针的链表
author: Jachin Lin
pub_date: 2020-01-21
tags:
    - 链表
    - Medium
difficulty: Medium
summary: 在复制普通链表的基础上，找到旧节点到新节点的映射关系用于更新新链表节点的随机指针。
---

## 描述 

[138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/)

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

![138. Copy List with Random Pointer](https://assets.leetcode.com/uploads/2019/12/18/e1.png)

## 思路

忽略随机指针的存在，复制一个普通链表非常简单。现在考虑随机指针，在复制普通链表的基础上，我们需要更新新链表中的随机指针，这个的关键在于找到 **旧节点到新节点的映射关系**。

简单的做法就是，把旧节点到新节点的映射关系存储在一个哈希表中，下边解法就是根据这个思路来的。

更高级的做法是，利用 **影子节点** ，将映射关系直接存储在新旧链表中，这样可以避免哈希表带来的 O(n) 额外空间。

## 解答

```python

# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random


class Solution:
    def copyRandomList(self, head: 'Node') -> 'Node':
        if not head:
            return
        node_map = {}  # old_node -> new_node
        new_head = new_tail = Node(-1)
        
        old_node = head
        while old_node:
            new_node = Node(old_node.val)
            new_node.random = old_node.random  # 复制旧的随机指针
            new_tail.next = new_node
            new_tail = new_tail.next
            node_map[old_node] = new_node
            old_node = old_node.next
        
        new_node = new_head.next
        while new_node:
            new_node.random = node_map.get(new_node.random)  # 更新随机指针
            new_node = new_node.next
        return new_head.next
        
```