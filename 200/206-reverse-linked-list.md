---
title: 反转链表
author: Jachin Lin
pub_date: 2019-08-20
tags:
    - 链表
---

[LeetCode 206](https://leetcode.com/problems/reverse-linked-list/)

## 思路

思路一，利用栈先进后出特点，时间 O(n)，空间 O(n)；

思路二，加一个头节点，遍历链表，将链表节点插入到头节点的下一个节点处，时间 O(n)，空间 O(1)；

思路三，双指针，时间 O(n)，空间 O(1)

## 解答

栈

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        stack = []
        while head:
            cur = head
            head = head.next
            cur.next = None
            stack.append(cur)
            
        head = cur = ListNode(None)
        while stack:
            cur.next = stack.pop()
            cur = cur.next
        return head.next
```

头节点

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        dummy = ListNode(None)
        while head:
            cur = head
            head = head.next
            cur.next = dummy.next
            dummy.next = cur
        return dummy.next
```

双指针

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if not head:
            return head
        pre, cur = head, head.next
        pre.next = None
        while cur:
            next_ = cur.next
            cur.next = pre
            pre, cur = cur, next_
        return pre
```

