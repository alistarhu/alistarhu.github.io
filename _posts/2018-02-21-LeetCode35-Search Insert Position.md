---
layout:     post
title:      35. Search Insert Position
subtitle:   
date:       2018-02-21
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 35. Search Insert Position - Easy

# Description
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

# Example
```
Example 1:
Input: [1,3,5,6], 5
Output: 2

Example 2:
Input: [1,3,5,6], 2
Output: 1

Example 3:
Input: [1,3,5,6], 7
Output: 4

Example 4:
Input: [1,3,5,6], 0
Output: 0
```

# Analysis
题目给定的条件是一个 **有序数组**，需要查找特定数字在数组中的位置，因此采用 **二分查找** 进行搜索

# Solution
```
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int left=0;
        int right=nums.size()-1;
        while(left<=right)
        {
            int mid=(left+right)/2;
            if(nums[mid]==target)
                return mid;
            else if(nums[mid]<target)
                left=mid+1;
            else
                right=mid-1;
        }
        return left;
    }
};
```
