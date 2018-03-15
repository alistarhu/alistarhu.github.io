---
layout:     post
title:      LeetCode 80. Remove Duplicates from Sorted Array II
subtitle:   
date:       2018-03-15
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 80. Remove Duplicates from Sorted Array II - Medium

# Description
Follow up for "Remove Duplicates":
What if duplicates are allowed at most twice?

# Example
```
For example,
Given sorted array nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.
```

# Analysis
题目要求将数组中重复次数超过2的元素删除（数组中元素最多允许重复两次），求删除后数组的长度。

# Solution
```
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size()<=2)
            return nums.size();
        int idx=2;
        for(int i=2;i<nums.size();i++)
        {
            if(nums[i]!=nums[idx-2])
                nums[idx++]=nums[i];
        }
        return idx;
    }
};
```
