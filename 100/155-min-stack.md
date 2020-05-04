---
title: 最小栈
author: Jachin Lin
pub_date: 2020-04-28
tags:
    - 链表
    - Easy
difficulty: Easy
summary: 使用辅助栈存储原始栈每个状态的最小值。
---

## 描述 

[155. Min Stack](https://leetcode.com/problems/min-stack/)

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.

## 思路

使用辅助栈存储原始栈每个状态的最小值。辅助栈中大部分值是相同的，有没有更优的做法呢？

## 解答

```python
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self._stack = []
        self._min_stack = []
        

    def push(self, x: int) -> None:
        self._stack.append(x)
        if not self._min_stack:
            min_ = x
        else:
            min_ = min(x, self._min_stack[-1])
        self._min_stack.append(min_)

    def pop(self) -> None:
        self._stack.pop()
        self._min_stack.pop()

    def top(self) -> int:
        return self._stack[-1]

    def getMin(self) -> int:
        return self._min_stack[-1]
```