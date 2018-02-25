---
layout:     post
title:      LeetCode 46. Permutations
subtitle:   
date:       2018-02-25
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 46. Permutations - Medium

# Description
Given a collection of distinct numbers, return all possible permutations.

# Example
```
For example, [1,2,3] have the following permutations:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

# Analysis
题目要求计算 **一个不含重复元素集合的全排列**。

这里采用回溯法思想，使用数组`visit`记录集合中哪些元素已经被使用过了哪些是当前可选的元素，`tmp_res`记录着全排列的中间结果。

全排列生成过程：首先确定第一个位置上的元素（从集合中选一个可用的元素，放到第一个位置上）。第一个元素确定之后，**原问题就由原先的求`n`个数的全排列变成了求`n-1`个数的全排列，即可以逐层向下递归调用……** 当tmp_res中元素个数与集合元素个数相同时，表明已经找到一个全排列，将结果保存下来。

# Solution
```
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> visit(nums.size(),0);
        vector<int> tmp;
        backtrack(res,nums,visit,tmp);
        return res;
    }

    void backtrack(vector<vector<int>>& res,vector<int>& nums,vector<int>& visit,vector<int>& tmp_res)
    {
        if(tmp_res.size()==nums.size())
            res.push_back(tmp_res);
        // Choose one num for current pos from the remain set
        for(int i=0;i<nums.size();i++)
        {
            if(visit[i]==0)
            {
                visit[i]=1;
                tmp_res.push_back(nums[i]);
                backtrack(res,nums,visit,tmp_res);
                // Reset
                visit[i]=0;
                tmp_res.pop_back();
            }
        }
    }
};
```
