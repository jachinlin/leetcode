---
title: 回文链表
author: Jachin Lin
pub_date: 2020-04-20
tags:
    - 链表
    - Easy
difficulty: Easy
summary: 原链表对半分成两个新的链表，反转转第二个链表，然后逐个比对这两个链表的元素。
---

## 描述 

[234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)

Given a singly linked list, determine if it is a palindrome.

## 思路

原链表对半分成两个新的链表，反转转第二个链表，然后逐个比较这两个链表的元素。

## 解答

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    
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
    
    def isPalindrome(self, head: ListNode) -> bool:
        if not head or not head.next:
            return True
        
        p, q = head, head.next
        while q and q.next and q.next.next:
            p = p.next
            q = q.next.next
            
        head2 = self._reverse(p.next)
        p.next = None
        
        while head and head2 and head.val == head2.val:
            head, head2 = head.next, head2.next
        
        if head and head2:
            return False
        return True
```
