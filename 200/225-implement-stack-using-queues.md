---
title: 使用两个队列实现栈
author: Jachin Lin
pub_date: 2020-05-03
tags:
    - 队列
    - 栈
    - Easy
difficulty: Easy
summary: 两个队列，一个队列存储元素，一个队列用来中转。
---

## 描述 

[225. Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/)

Implement the following operations of a stack using queues.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- empty() -- Return whether the stack is empty.

## 思路

使用两个队列，一个队列 q 存储元素，一个队列 tmp 用来中转。

push(x) 时，先将 x push 到 tmp，然后把 q 中的元素全部弹出 push 到 tmp 中，最后交换 q、tmp 指针，时间复杂度 O(n)。
pop() 时，直接 pop q，时间复杂度 O(1)。

另一种思路是，push(x) 直接 push 到 q，时间复杂度 O(1)。
pop() 时先将 q 中除了队尾的其他元素弹出 push 到 tmp 中，然后弹出 q 队尾元素，最后交换 q、tmp 指针，时间复杂度 O(n)。


## 解答


```python
class MyStack:

    def __init__(self):
        self._q = []  # using list as queue
        self._tmp = []
        

    def push(self, x: int) -> None:
        self._tmp.append(x)
        while self._q:
            self._tmp.append(self._q.pop(0))
        self._q, self._tmp = self._tmp, self._q

    def pop(self) -> int:
        return self._q.pop(0)
        

    def top(self) -> int:
        return self._q[0]
        

    def empty(self) -> bool:
        return not self._q
```

