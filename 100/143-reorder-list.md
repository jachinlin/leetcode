---
title: 重排链表
author: Jachin Lin
pub_date: 2020-04-17
tags:
    - 链表
    - Medium
difficulty: Medium
summary: 原链表对半分成两个链表，反转第二个链表，然后合并这两个链表。
---

## 描述 

[143. Reorder List](https://leetcode.com/problems/reorder-list/)

Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You may not modify the values in the list's nodes, only nodes itself may be changed.
## 思路

找到中间节点，断开成两个新的链表，反转后半截的链表，然后合并这两个两个链表。

## 解答

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    
    def _merge2List(self, list1, list2):
        dummy = tail = ListNode(-1)
        while list1 and list2:
            tmp1, tmp2 = list1, list2
            list1, list2 = list1.next, list2.next
            tail.next = tmp1
            tmp1.next = tmp2
            tail = tmp2
        tail.next = list1 or list2
        
        return dummy.next
    
    def _reverse(self, head: ListNode):
        if not head or not head.next:
            return head
        p, q = head, head.next
        p.next = None
        while q:
            next_ = q.next
            q.next = p
            p, q = q, next_
        return p
    
    def reorderList(self, head: ListNode) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        if not head or not head.next:
            return
        p, q = head, head.next
        while q and q.next and q.next.next:
            p = p.next
            q = q.next.next
        
        head2 = self._reverse(p.next)
        p.next = None
        self._merge2List(head, head2)
        
```