---
title: 两两交换链表节点
author: Jachin Lin
pub_date: 2019-01-01
difficulty: Medium
summary: 双指针，q 在前，p 在后，交换 p、q；然后 p、 q 一起向后走两步，交换 p、q；重复操作至到 q 走到链表末尾。
tags:
    - 链表
    - Medium
---

## 描述
[24. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)

Given a linked list, swap every two adjacent nodes and return its head.

You may not modify the values in the list's nodes, only nodes itself may be changed.## 思路

## 思路
双指针，q 在前，p 在后，交换 p、q；然后 p、 q 一起向后走两步，交换 p、q；重复操作至到 q 走到链表末尾。

## 解答

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        dummy = ListNode(-1)
        dummy.next = head
        o, p, q = dummy, head, head.next
        while True:
            # swap
            o.next = q
            p.next = q.next
            q.next = p
            p, q = q, p
            # forward
            if q.next and q.next.next:
                o = o.next.next
                p = p.next.next
                q = q.next.next
            else:
                break
        return dummy.next
```