---
title: 实现 atoi 函数
author: Jachin Lin
pub_date: 2019-09-01
summary: 递归，f(n) = f(n-1) * 10 + int(str[n]), 边界 f(0) = int(str[0]), f(n) 表示 str[0, n] (闭区间)转化后的整数。
difficulty: Medium
tags:
    - Medium
---

## 描述
[8. String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

Implement atoi which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned.

Note:
- Only the space character ' ' is considered as whitespace character.
- Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.

## 思路

忽略各种异常输入，只考虑有效输入。运用 **递归** 这种减而治之的思想，很容易得到下方这条方程：

> `f(n) = f(n-1) * 10 + int(str[n])`，边界 `f(0) = int(str[0])`

f(n) 表示 str[0, n] (闭区间)转化后的整数。

## 解答

```python
class Solution:
    
    def _digit2int(self, digit):
        return ord(digit) - 48  # ord('0') = 48
    
    def _clear(self, str):
        if not str:
            return 0, 0, 0
        left, right, length = 0, 0, len(str)
        while left < length and str[left] == ' ':
            left += 1
        if left == length:
            return 0, 0, 0
        if str[left] == '-':
            sign = -1
            left += 1
        elif str[left] == '+':
            sign = 1
            left += 1
        else:
            sign = 1
        right = left
        while right < length and str[right].isdigit():
            right += 1
        return left, right, sign
    
    def _myAtoi(self, str, left, right) -> int:
        if left >= right:
            return 0
        return self._myAtoi(str, left, right-1) * 10 + self._digit2int(str[right-1])

    def myAtoi(self, str: str) -> int:
        left, right, sign = self._clear(str)
        res = self._myAtoi(str, left, right) * sign
        min_ = - (1 << 31)
        max_ = (1 << 31) - 1
        if res > max_:
            return max_
        if res < min_:
            return min_
        return res
```