---
title: 最长括号匹配
author: Jachin Lin
pub_date: 2020-05-01
difficulty: Hard
summary: 使用栈，遇到左括号则入栈，右括号则出栈，栈元素为括号下标。使用变量 last 表示有效括号对的左边界，当括号不匹配时更新 last 值，括号匹配时更新 max_longest。
tags:
    - 栈
    - Hard
---

## 描述
[32. Longest Valid Parentheses](https://leetcode.com/problems/longest-valid-parentheses/)

Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

test cases: `()(()`、`()()(`

## 思路

使用栈，遇到左括号则入栈，右括号则出栈。
一、因为只有 '()' 一种括号，栈元素可以改为括号下标，以存储更多的信息，然后使用一个变量 last 来表示有效括号对的左边界，当括号不匹配时更新 last 的值。
二、什么时候计算当前最大值 this_longest 呢？当括号不匹配时呢，还是括号匹配时计算呢。分析 case `()(()`，发现当括号匹配时更新 this_longest 时更易判断。

## 解答

```python
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        
        stack = []
        longest = 0
        last = -1
        
        for i, c in enumerate(s):
            if c == '(':
                stack.append(i)
            elif not stack:
                last = i
            else:
                stack.pop()
                if not stack:
                    longest = max(longest, i - last)
                else:
                    longest = max(longest, i - stack[-1])                
        
        return longest
```