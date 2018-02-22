---
layout:     post
title:      LeetCode 40. Combination Sum II
subtitle:   
date:       2018-02-22
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 40. Combination Sum II - Medium

# Description
Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

Each number in C may only be used once in the combination.

**Note:** All numbers (including target) will be positive integers.The solution set must not contain duplicate combinations.

# Example
```
For example, given candidate set [10, 1, 2, 7, 6, 1, 5] and target 8, A solution set is:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

# Analysis
- 这道题与`Leetcode40-Combination Sum`的解法类似，都是采用 **回溯法** 思想
- 这道题的不同之处在于 **集合中重复的数字出现**、**每个数字只能使用一次**，由于集合中存在了重复数字那么 **如何在搜索过程中去除重复解成为了这道题的关键**。
- 去重方法：假设集合为`12223`，target=6，假设我们第一层遍历在path中加入了`3`，在向下递归进入下一层时共有`2`、`2`、`2`、`1`等4中选择，其中的三个`2`则会引起重复解，因此为了避免重复解的出现，我们在 **同一层的递归中对于相同数字只使用一次（只使用最靠右侧的那个重复数字）**，通过`j==start-1||candidates[j]!=candidates[j+1]`条件来实现重复解剔除

# Solution
```
class Solution {
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        std::sort(candidates.begin(),candidates.end());
        vector<vector<int>> res;
        vector<int> path;
        find(res,candidates,path,target,candidates.size());
        return res;
    }

    void find(vector<vector<int>>& res,vector<int>& candidates,vector<int>& path,int target,int start)
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
            int j=start-1;///
            for(;j>=0;j--)
            {
                if((j==start-1||candidates[j]!=candidates[j+1])&&candidates[j]<=target)///
                {
                    path.push_back(j);
                    find(res,candidates,path,target-candidates[j],j);
                    path.pop_back();
                }
            }
        }
    }
};
```
