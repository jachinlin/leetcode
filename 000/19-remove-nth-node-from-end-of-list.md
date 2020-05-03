---
title: 删除链表倒数第 n 个节点
author: Jachin Lin
pub_date: 2019-12-21
difficulty: Medium
summary: 双指针，q 指针比 p 指针多走 n 步。
tags:
    - 链表
    - Medium
---

## 描述
[19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

Given a linked list, remove the n-th node from the end of list and return its head.
## 思路

朴素的做法，先遍历一遍得到链表长度 l，然后再遍历一遍，删掉第 l - n 个节点。时间复杂度 O(2n) = O(n)，可以接受。

只需要遍历一遍的做法是利用双指针，q 指针先走 n 步，然后 p、q 指针一起向后走，指导 q 指针走到链表末尾。然后删掉 p 指针的下一个节点。

## 解答

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        
        dummy = ListNode(-1)
        dummy.next = head
        
        p, q = dummy, head
        
        for i in range(n):
            q = q.next  # raise directly
        
        while q:
            p, q = p.next, q.next
        
        p.next = p.next.next
        
        return dummy.next
```