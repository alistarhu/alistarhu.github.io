---
layout:     post
title:      LeetCode 64. Minimum Path Sum
subtitle:   
date:       2018-03-09
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 64. Minimum Path Sum - Medium

# Description
Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

# Example
```
For example,
[[1,3,1],
 [1,5,1],
 [4,2,1]]
Given the above grid map, return 7. Because the path 1→3→1→1→1 minimizes the sum.
```

# Analysis
这道题与`LeetCode62-Unique Paths`思路类似，都是采用动态规划思想，这里需要计算最小路径和，递推公式变为了：`dp[i][j]=min(dp[i-1][j],dp[i][j-1])+grid[i][j]`

# Solution
```
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m=grid.size();
        int n=grid[0].size();
        vector<vector<int>> dp(m,vector<int>(n,0));
        dp[0][0]=grid[0][0];
        for(int i=1;i<m;i++)
            dp[i][0]=dp[i-1][0]+grid[i][0];
        for(int j=1;j<n;j++)
            dp[0][j]=dp[0][j-1]+grid[0][j];
        for(int i=1;i<m;i++)
            for(int j=1;j<n;j++)
                dp[i][j]=min(dp[i-1][j],dp[i][j-1])+grid[i][j];
        return dp[m-1][n-1];
    }
};
```
