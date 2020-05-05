---
title: 逆波兰表达式求值
author: Jachin Lin
pub_date: 2020-05-02
summary: 使用栈，遇到操作数则入栈，操作符则出栈计算再把结果入栈
difficulty: Medium
tags:
    - 栈
    - Medium
---

## 描述

[150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

Evaluate the value of an arithmetic expression in Reverse Polish Notation.

Valid operators are +, -, *, /. Each operand may be an integer or another expression.

## 思路

使用栈，遇到操作数则入栈，操作符则出栈计算再把结果入栈，最后栈顶元素即为表达式的值。

## 解答

```python
from typing import List

class Solution:
    _ops = ('+', '-', '*', '/')
    
    def _calculate(self, op, num1, num2):
        if op == '+':
            return num1 + num2
        elif op == '-':
            return num1 - num2
        elif op == '*':
            return num1 * num2
        else:
            return int(num1 / num2)
        
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []
        for t in tokens:
            if t not in self._ops:
                stack.append(int(t))
            else:
                b = stack.pop()
                a = stack.pop()
                res = self._calculate(t, a, b)
                stack.append(res)
        return stack.pop()

```