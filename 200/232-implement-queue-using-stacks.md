---
title: 使用两个栈实现队列
author: Jachin Lin
pub_date: 2020-05-04
tags:
    - 队列
    - 栈
    - Easy
difficulty: Easy
summary: 两个栈，一个栈存储元素，一个栈用来中转。
---

## 描述 

[232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)

Implement the following operations of a queue using stacks.

- push(x) -- Push element x to the back of queue.
- pop() -- Removes the element from in front of queue.
- peek() -- Get the front element.
- empty() -- Return whether the queue is empty.

## 思路

使用两个栈，一个栈 stack 存储元素，一个栈 tmp 用来中转。

push(x) 时，先把 stack 中的元素全部弹出 push 到 tmp 中，然后 push x 到 stack，再把 tmp 中元素弹出归还 stack，时间复杂度 O(n)。
pop() 时，直接 pop stack，时间复杂度 O(1)。

另一种思路是，push 时直接 push，pop 时利用 tmp 中转，思路和上面类似。不过 push(x) 时间复杂度 O(1)，pop() 时间复杂度 O(n)。


## 解答


```python
class MyQueue:

    def __init__(self):
        self._stack = []  # using list as stack
        self._tmp = []
        

    def push(self, x: int) -> None:
        while self._stack:
            self._tmp.append(self._stack.pop())
        self._stack.append(x)
        while self._tmp:
            self._stack.append(self._tmp.pop())
        

    def pop(self) -> int:
        return self._stack.pop()
        

    def peek(self) -> int:
        return self._stack[-1]
        

    def empty(self) -> bool:
        return not self._stack
```

