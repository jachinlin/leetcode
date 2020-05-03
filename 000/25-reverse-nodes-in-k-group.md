---
title: k 个一组翻转链表
author: Jachin Lin
pub_date: 2020-02-20
difficulty: Hard
summary: 递归，f(n) = reverse(link[1, k]) + f(n-k)
tags:
    - 链表
    - Hard
---

## 描述
[25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)

Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

## 思路

递归，f(n) = reverse(link[1, k]) + f(n-k)。需要注意的是，每个分组中不能使用 **头节点** 的方式进行反转段链表，使用空头节点的话，空间复杂度为 O(n/k) = O(n) 。

## 解答

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution:
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
        if not head or not head.next or k < 2:
            return head
        new_group = head
        for i in range(k):
            if new_group:
                new_group = new_group.next
            else:
                return head
            
        pre, cur = head, head.next
        this_group_tail  = pre
        for i in range(k - 1):
            next_ = cur.next
            cur.next = pre
            pre, cur = cur, next_
        this_group_tail.next = self.reverseKGroup(cur, k)
        
        return pre
```