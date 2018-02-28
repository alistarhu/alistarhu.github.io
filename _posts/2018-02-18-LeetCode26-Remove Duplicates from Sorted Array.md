---
layout:     post
title:      LeetCode 26. Remove Duplicates from Sorted Array
subtitle:   
date:       2018-02-18
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 26. Remove Duplicates from Sorted Array - Easy

# Description
Given a sorted array, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

# Example
```
For example,
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
It doesn't matter what you leave beyond the new length.
```

# Analysis
- 题目要求将数组中的重复元素删去并且不允许开辟额外空间，因此我们需要在原始数组上进行数据操作（不能额外开辟一个新数组，将旧数组复制到新数组中）。
- 这里采用的思路：定义两个游标，一个从前向后扫描整个数组，另一个游标定位在删除重复元素后的位置

# Solution
```
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size()<2)
            return nums.size();
        int idx=1;
        for(int i=1;i<nums.size();i++)
        {
            if(nums[i]!=nums[i-1])
            {
                nums[idx]=nums[i];
                idx++;
            }
        }
        return idx;
    }
};
```
