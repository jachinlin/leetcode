---
title: 链表是否存在环，存在的话找出环的入口？
author: Jachin Lin
pub_date: 2020-03-04
tags:
    - 链表
    - Medium
difficulty: Medium
summary: 当快(fast)慢(slow)指针相遇时，如果此时有新的一个慢(slow2)指针从表头出发，两个慢指针将在环入口处相遇。
---

## 描述 

[142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)

Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

## 思路

在 [链表是否存在环](./141-linked-list-cycle.html) 的基础上，当快(fast)慢(slow)指针相遇时，如果此时有新的一个慢(slow2)指针从表头出发，会发什么呢？
**两个指针将在原先快慢指针相遇的地方相遇。**

为什么？

假设，当时间为 t 时，快慢指针第一次相遇，此时快指针前进的节点数为 2t，慢指针 slow 前进的节点数为 t。
当时间为 2t 时，慢指针 slow 前进的节点数为 2t，慢指针 slow2 前进的节点数为 t。

发现没？此时两个慢指针前进的节点数和快慢指针第一次相遇时前进的节点数是一样的。
也就是说，两个慢指针将会在快慢指针相遇的地方相遇，回退几步，两个慢指针也会在环入口处相遇。
换句话说，**两个慢指针第一次相遇的地方就是环入口**。

## 解答

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        if not head or not head.next or not head.next.next:
            return None
        slow = fast = head
        while fast.next and fast.next.next:
            slow = slow.next
            fast = fast.next.next
            if slow is fast:
                break
        if slow is not fast:
            return None
        
        slow2 = head
        while slow2 is not slow:
            slow2 = slow2.next
            slow = slow.next
        return slow2
        
```