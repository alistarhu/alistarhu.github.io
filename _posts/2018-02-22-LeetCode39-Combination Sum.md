---
layout:     post
title:      LeetCode 39. Combination Sum
subtitle:   
date:       2018-02-22
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 39. Combination Sum - Medium

# Description
Given a **set** of candidate numbers **(C) (without duplicates)** and a target number (**T**), find all unique combinations in **C** where the candidate numbers sums to **T**.

The **same** repeated number may be chosen from **C** unlimited number of times.

**Note:** All numbers (including target) will be positive integers.The solution set must not contain duplicate combinations.

# Example
```
For example, given candidate set `[2, 3, 6, 7]` and target `7`, A solution set is:
[
  [7],
  [2, 2, 3]
]
```

# Analysis
这道题要求和为定值的组合数，这里采用 **回溯法** 思想，首先将数组从小到大排好序，然后从右向左确定组合数中的第一个元素，如果元素和没有达到target则继续向下递归搜索；如果不满足条件则舍弃；如果找到一个可行解则将结果保存下来。

# Solution
```
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        std::sort(candidates.begin(),candidates.end());
        vector<vector<int>> res;
        for(int i=candidates.size()-1;i>=0;i--)
        {
            if(candidates[i]<=target)
            {
                vector<int> path;
                path.push_back(i);
                find(res,candidates,path,target-candidates[i]);
            }
        }
        return res;
    }

    void find(vector<vector<int>>& res,vector<int>& candidates,vector<int>& path,int target)
    {
        if(target==0)
        {
            vector<int> tmp;
            for(int i=path.size()-1;i>=0;i--)
                tmp.push_back(candidates[path[i]]);
            res.push_back(tmp);
        }
        else if(target>0)
        {
            int j=path.back();
            for(;j>=0;j--)
            {
                if(candidates[j]<=target)
                {
                    path.push_back(j);
                    find(res,candidates,path,target-candidates[j]);
                    path.pop_back();
                }
            }
        }
    }
};
```
