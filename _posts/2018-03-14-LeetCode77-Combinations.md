---
layout:     post
title:      LeetCode 77. Combinations
subtitle:   
date:       2018-03-14
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 77. Combinations - Medium

# Description
Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

# Example
```
For example,
If n = 4 and k = 2, a solution is:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

# Analysis
这道题需要求组合数，这里采用回溯法逐层递归进行求解。（求全排列、组合数的方法都类似）

具体做法：
- 由于组合数不考虑顺序，我们在搜索答案时，一个组合数中元素都是由小到大排列的。这里使用backtrack作为递归函数，`path`变量存储着组合数的中间形态
- 在每一轮递归调用backtrack时都会向path中插入一个元素，插入的元素是从当前path中最后一个元素(假设为i)之后的元素中选一个插入(i+1~n选一个)。
- 如果`path.size()==k`时，表明我们已经找到了一个组合数，将其插入res中

# Solution
```
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> res;
        vector<int> path;
        backtrack(res,path,n,k,0);
        return res;
    }

    void backtrack(vector<vector<int>>& res,vector<int>& path,int n,int k,int start)
    {
        if(path.size()==k)
            res.push_back(path);
        else
        {
            for(int i=start;i<n;i++)
            {
                path.push_back(i+1);
                backtrack(res,path,n,k,i+1);
                path.pop_back();
            }
        }
    }
};
```
