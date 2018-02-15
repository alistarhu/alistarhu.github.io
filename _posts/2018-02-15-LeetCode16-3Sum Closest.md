---
layout:     post
title:      LeetCode 16. 3Sum Closest
subtitle:   
date:       2018-02-15
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 16. 3Sum Closest - Medium

# Description
Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

# Example
```
For example, given array S = {-1 2 1 -4}, and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

# Analysis
这道题与`Leetcode15-3sum`方法相似，都是先将数组排序，再固定一个元素，由两端向中间搜索剩下的两个元素，要求3sum与target尽可能接近。

# Solution
```
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        if(nums.size()<3)
            return 0;
        int res=nums[0]+nums[1]+nums[2];
        sort(nums.begin(),nums.end());
        for(int i=0;i<nums.size()-2;i++)
        {
            int lo=i+1;
            int he=nums.size()-1;
            while(lo<he)
            {
                int sum=nums[lo]+nums[he]+nums[i];
                // Find one near result
                if(abs(sum-target)<abs(res-target))
                    res=sum;
                if(sum<target)
                    lo++;
                else if(sum>target)
                    he--;
                else
                    break;
            }
        }
        return res;
    }
};
```
