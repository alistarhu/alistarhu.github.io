---
layout:     post
title:      LeetCode 78. Subsets
subtitle:   
date:       2018-03-14
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 78. Subsets - Medium

# Description
Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

# Example
```
For example,
If nums = [1,2,3], a solution is:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

# Analysis
这道题需要所有可能的子集。这道题依然使用回溯法，与`LeetCode77`解法类似，其实就是相当于求n个数的0、1、2……n个组合数，**由于组合数直接具有包含关系如果直接进行n+1个循环则会有重复计算出现**，其实我们在求解n的组合数时中间变量的状态就是一个解，我们在每轮递归过程中都把中间变量结果加入res中即可。

# Solution
```
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> path;
        backtrack(nums,res,path,0);
        return res;
    }

    void backtrack(vector<int>& nums,vector<vector<int>>& res,vector<int>& path,int start)
    {
        res.push_back(path);
        for(int i=start;i<nums.size();i++)
        {
            path.push_back(nums[i]);
            backtrack(nums,res,path,i+1);
            path.pop_back();
        }
    }
};
```
