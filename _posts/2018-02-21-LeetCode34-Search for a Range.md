---
layout:     post
title:      34. Search for a Range
subtitle:   
date:       2018-02-21
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 34. Search for a Range - Medium

# Description
Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return `[-1, -1]`.

# Example
```
Given [5, 7, 7, 8, 8, 10] and target value 8,
return [3, 4].
```

# Analysis
题目要求时间复杂度控制在O(log n)，因此使用两次二分查找，第一次查找最靠近左侧的目标数，第二次查找最靠近右侧的目标数。

这里在求右侧坐标mid时有个小trick，**mid需要设成`(left+right)/2+1`**，这样能够让查找更倾向于向右侧搜索，能够避免`ab`在查找`a`时陷入死循环，能够使左右坐标相遇从而收敛

# Solution
```
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> res(2,-1);
        if(nums.size()==0)
            return res;
        int left=0;
        int right=nums.size()-1;
        // Find left position
        while(left<right)
        {
            int mid=(left+right)/2;
            if(nums[mid]<target)
                left=mid+1;
            else if(nums[mid]>target)
                right=mid-1;
            else
                right=mid;
        }
        if(target!=nums[left])
            return res;
        else
            res[0]=left;

        // Find right position
        right=nums.size()-1;
        while(left<right)
        {
            int mid=(left+right)/2+1;
            if(nums[mid]<target)
                left=mid+1;
            else if(nums[mid]>target)
                right=mid-1;
            else
                left=mid;
        }
        res[1]=right;
        return res;
    }
};
```
