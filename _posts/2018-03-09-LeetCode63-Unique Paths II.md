---
layout:     post
title:      LeetCode 63. Unique Paths II
subtitle:   
date:       2018-03-09
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 63. Unique Paths II - Medium

# Description
Follow up for "Unique Paths":

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as `1` and `0` respectively in the grid.

# Example
```
For example,
There is one obstacle in the middle of a 3x3 grid as illustrated below.
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
The total number of unique paths is 2.
```

# Analysis
这道题与上一道题解法相同，只不过这里加了一个限制条件：**有些位置不能走**

我们只需要在迭代的时候加一个判断条件即可：`if(obstacleGrid[i][j]!=1)`则进行计算`dp[i][j]=dp[i-1][j]+dp[i][j-1]`;否则，直接在dp[i][j]上赋0即可。

# Solution
```
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m=obstacleGrid.size();
        int n=obstacleGrid[0].size();
        vector<vector<int>> dp(m,vector<int>(n,0));
        if(obstacleGrid[0][0]!=1)
            dp[0][0]=1;
        for(int i=1;i<m;i++)
            if(obstacleGrid[i][0]!=1)
                dp[i][0]=dp[i-1][0];
        for(int j=1;j<n;j++)
            if(obstacleGrid[0][j]!=1)
                dp[0][j]=dp[0][j-1];
        for(int i=1;i<m;i++)
        {
            for(int j=1;j<n;j++)
            {
                if(obstacleGrid[i][j]!=1)
                    dp[i][j]=dp[i-1][j]+dp[i][j-1];
            }
        }       
        return dp[m-1][n-1];
    }
};
```
