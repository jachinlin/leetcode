---
title: 删除排序链表中的重复元素
author: Jachin Lin
pub_date: 2019-09-21
difficulty: Easy
summary: 使用一个指针指向目标链表的末尾，遍历原链表，如果原链表元素与目标链表尾元素不同，则把该元素添加到目标链表末尾。
tags:
    - 数组
    - Easy
---

## 描述
[83. Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/)

Given a sorted linked list, delete all duplicates such that each element appear only once.


## 思路

思路同删除排序数组中的重复元素。使用一个指针指向目标链表的末尾，遍历原链表，如果原链表元素与目标链表尾元素不同，则把该元素添加到目标链表末尾。

## 解答

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        if not head:
            return head
        index, next_ = head, head.next
        while next_:
            if next_.val != index.val:
                index.next = next_
                index = index.next
            next_ = next_.next
        index.next = None
        return head
```