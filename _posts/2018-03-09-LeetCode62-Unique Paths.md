---
layout:     post
title:      LeetCode 62. Unique Paths
subtitle:   
date:       2018-03-09
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 62. Unique Paths - Medium

# Description
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

# Example
```

```

# Analysis
题目需要求从一个矩阵的左上角走到其右下角总的方法数。这里使用动态规划思想。

使用数组`dp[i][j]`记录着从左上角即坐标`(0,0)`走到`(i,j)`的方法数。由于从当前位置向后移动 **只能向右或是向下运动**
- 对于第一行和第一列的元素都有`dp[0][j]=dp[i][0]=1`
- 对于其他位置`(i,j)`元素，由于想要到达当前位置(i,j)只可能从其上方或是左方过来，所以有关系式`dp[i][j]=dp[i-1][j]+dp[i][j-1]`
- dp[m-1][n-1]即为所求

# Solution
```
class Solution {
public:
    int uniquePaths(int m, int n) {
        int dp[m][n]={0};
        for(int i=0;i<m;i++)
            dp[i][0]=1;
        for(int j=0;j<n;j++)
            dp[0][j]=1;
        for(int i=1;i<m;i++)
            for(int j=1;j<n;j++)
                dp[i][j]=dp[i-1][j]+dp[i][j-1];
        return dp[m-1][n-1];
    }
};
```
