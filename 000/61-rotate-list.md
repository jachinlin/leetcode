---
title: 旋转链表
author: Jachin Lin
pub_date: 2019-10-15
difficulty: Medium
summary: 把链表变成环，然后再从 length - k 出断开。
tags:
    - 链表
    - Medium
---

## 描述
[61. Rotate List](https://leetcode.com/problems/rotate-list/)

Given a linked list, rotate the list to the right by k places, where k is non-negative.

## 思路

遍历链表，计算链表长度 l，并把链表变成环，然后从 l-k 出断开即可获取旋转后的链表。

## 解答

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution:
    def rotateRight(self, head: ListNode, k: int) -> ListNode:
        if not head:
            return head
        length = 1
        cur = head
        while cur.next:
            length += 1
            cur = cur.next
            
        cur.next = head
        for i in range(length - k % length - 1):
            head = head.next
        
        new_head = head.next
        head.next = None
        return new_head
```