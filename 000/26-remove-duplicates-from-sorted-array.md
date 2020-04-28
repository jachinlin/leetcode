---
title: 删除排序数组中的重复元素
author: Jachin Lin
pub_date: 2019-09-08
difficulty: Easy
summary: 目标数组复用原数组空间
tags:
    - 数组
---

## 描述
[26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

## 思路

假设可以使用额外空间，解法就很简单了，使用一个新的数组，称为目标数组。
遍历原数组，将遍历到的元素同目标数组最后一个元素进行对比，不一样就添加到目标数组末尾。

其实，原数组遍历过的元素所占有的空间已经没有用处了，我们可以这些空间用作目标数组的空间，这样就不需要额外的内存空间了。目标数组直接覆盖原数组元素即可。逻辑上还是两个数组，实际上是同一片内存空间。

## 解答

```python
from typing import List


class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if not nums:
            return 0
        index = 0
        for i in range(1, len(nums)):
            if nums[i] != nums[index]:
                index += 1
                nums[index] = nums[i]
        return index + 1
```