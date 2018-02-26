---
layout:     post
title:      LeetCode 53. Maximum Subarray
subtitle:   
date:       2018-02-26
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 53. Maximum Subarray - Easy

# Description
Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

# Example
```
For example,
given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.
```

# Analysis
这道题要求计算和最大的子数组。

这里采用动态规划思想，dp[i]记录着到第i个元素为止的最大子数组和，dp[i]的值与dp[i-1]的值有关：如果dp[i-1]<0,dp[i]=nums[i]，即以第i个元素为止的子数组在只有一个元素（nums[i]本身）时取最大和（因为如果带上之前的元素只会让总和变小）；如果dp[i-1]>0,dp[i]=dp[i-1]+nums[i]。这样只需要扫描一遍数组就可以找出子数组中和的最大值。

# Solution
```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        vector<int> dp(nums.size(),0);
        int max=nums[0];
        dp[0]=nums[0];
        for(int i=1;i<nums.size();i++)
        {
            if(dp[i-1]<0)
                dp[i]=nums[i];
            else
                dp[i]=nums[i]+dp[i-1];
            if(dp[i]>max)
                max=dp[i];
        }
        return max;
    }
};
```
