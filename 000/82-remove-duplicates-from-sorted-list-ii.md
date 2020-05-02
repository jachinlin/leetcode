---
title: 删除排序链表中的重复元素 II
author: Jachin Lin
pub_date: 2019-09-28
difficulty: Medium
summary: 递归，需要分 head.val == next.val 和 head.val != next.val 两种情况考虑。
tags:
    - 链表
    - Medium
---

## 描述
[82. Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)

Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

Return the linked list sorted as well.

## 思路

递归，需要分 head.val == next.val 和 head.val != next.val 两种情况。

## 解答

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        
        if head.val == head.next.val:
            while head.next and head.val == head.next.val:
                head = head.next
            return self.deleteDuplicates(head.next)
        
        head.next = self.deleteDuplicates(head.next)
        return head
```