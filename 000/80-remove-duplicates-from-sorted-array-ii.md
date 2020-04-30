---
title: 删除排序数组中的重复元素 II
author: Jachin Lin
pub_date: 2019-09-18
difficulty: Medium
summary: 在「删除排序数组中的重复元素」解法的基础上，增加一个变量表示目标数组中末尾元素已经出现的次数。
tags:
    - 数组
    - Medium
---

## 描述
[80. Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)

Given a sorted array nums, remove the duplicates in-place such that duplicates appeared at most twice and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

## 思路

在[删除排序数组中的重复元素](./26-remove-duplicates-from-sorted-array.html)解法的基础上，增加一个变量表示目标数组中末尾元素已出现的次数，根据该变量的大小来判断原数组下一个元素是否为目标数组的元素。
更取巧的做法是，`nums[i]` 直接和 `nums[i-2]` 对比，两者不同，则 `nums[i]` 为目标数组的元素。

## 解答

```python
from typing import List


class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if not nums:
            return 0
        length = len(nums)
        if length < 3:
            length
        index = 1
        for i in range(2, length):
            if nums[i] != nums[index - 1]:
                index += 1
                nums[index] = nums[i]
        return index + 1
        
```