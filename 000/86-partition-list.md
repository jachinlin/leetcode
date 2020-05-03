---
title: 分割链表
author: Jachin Lin
pub_date: 2019-11-02
difficulty: Medium
summary: 两个头节点
tags:
    - 链表
    - Medium
---

## 描述
[86. Partition List](https://leetcode.com/problems/partition-list/)

Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.
## 思路

利用两个头节点把分割后的节点串成两个新链表，然后把两个链表串起来就好了。

## 解答

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution:
    def partition(self, head: ListNode, x: int) -> ListNode:
        dummy1 = left = ListNode(-1)
        dummy2 = right = ListNode(-1)
        
        while head:
            if head.val < x:
                left.next = head
                left = left.next
            else:
                right.next = head
                right = right.next
            head = head.next
        right.next = None
        left.next = dummy2.next
        
        return dummy1.next
```