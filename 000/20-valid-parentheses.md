---
title: 括号匹配
author: Jachin Lin
pub_date: 2020-04-22
difficulty: Easy
summary: 使用栈，遍历字符串，遇到左括号则入栈，右括号则出栈比对。
tags:
    - 栈
    - Easy
---

## 描述
[20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.

## 思路

使用栈，遍历字符串，遇到左括号则入栈，右括号则出栈比对。

## 解答

```python
class Solution:
    _parentheses = {
        ')': '(', '}': '{', ']': '[' 
    }
    
    def isValid(self, s: str) -> bool:
        stack = []
        for c in s:
            if c in ('(', '{', '['):
                stack.append(c)
            else:
                if not stack:
                    return False
                cc = stack.pop()
                if cc != self._parentheses.get(c):
                    return False
        if stack:
            return False
        return True
```