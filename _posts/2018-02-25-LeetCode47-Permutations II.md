---
layout:     post
title:      LeetCode 47. Permutations II
subtitle:   
date:       2018-02-25
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 47. Permutations II - Medium

# Description
Given a collection of numbers that might contain duplicates, return all possible unique permutations.

# Example
```
For example, [1,1,2] have the following unique permutations:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

# Analysis
题目要求计算 **一个含有重复元素集合的全排列**，这道题与`LeetCode-47Permutations`解法相同，唯一的不同在于 **集合中存在了重复元素，在生成全排列时需要去除重复解**。

分析造成重复解的原因：如果在同一个位置上使用了值相同的元素，则会造成重复计算。因此在 **同一个位置上(同一轮递归中)值相同的元素只能使用一次**，

程序实现：为了方便去重，我们首先需要将数组统一排序，使得重复的元素位置上保持连续性。某个位置在选择元素填充时，我们默认只使用重复元素中的第一个元素，之后的重复元素满足`visit[i-1]==0&&nums[i]==nums[i-1]`的条件需要跳过（`nums[i]==nums[i-1]`表示值相同，`visit[i-1]==0`表示所处于同一轮递归,，前一个重复元素已经在该轮递归中被使用过一次了）。

# Solution
```
class Solution {
public:
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(),nums.end());
        vector<int> visit(nums.size(),0);
        vector<int> tmp_res;
        backtrack(res,nums,visit,tmp_res);
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
                // Filter the dumplicate result in the same level
                if(i>0&&visit[i-1]==0&&nums[i]==nums[i-1])
                    continue;
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
