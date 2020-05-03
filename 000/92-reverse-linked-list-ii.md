---
title: 反转链表 II
author: Jachin Lin
pub_date: 2019-11-04
tags:
    - 链表
    - Medium
difficulty: Medium
summary: 双指针，指针 p 指向反转段的上一个节点，指针 q 指向反转段的最后一个节点。
---

## 描述 

[92. Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/)

Reverse a linked list from position m to n. Do it in one-pass.

Note: 1 ≤ m ≤ n ≤ length of list.

## 思路

添加空头节点，可以减少好多边界判断。然后利用双指针，指针 p 指向反转段的上一个节点，指针 q 指向反转段的最后一个节点。

遍历原链表，如果遍历的长度 l < m，则 p 指向该节点；如果 l == m，则 p 保持不变不往后移动了，q 指向当前节点；
如果 m < l <= n，把该节点插入到 p 节点后边；如果 l > n，则把剩下的直接加到 q 的后边。

## 解答

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def reverseBetween(self, head: ListNode, m: int, n: int) -> ListNode:
        
        dummy = ListNode(-1)
        p = dummy
        cur = head
        for i in range(m - 1):
            p.next = cur
            p = p.next
            cur = cur.next
        
        q = cur
        for i in range(n - m + 1):
            next_ = cur.next
            cur.next = p.next
            p.next = cur
            cur = next_
            
        q.next = cur
        
        return dummy.next
```

