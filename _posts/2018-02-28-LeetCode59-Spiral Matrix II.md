---
layout:     post
title:      LeetCode 59. Spiral Matrix II
subtitle:   
date:       2018-02-28
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 59. Spiral Matrix II - Medium

# Description
Given an integer n, generate a square matrix filled with elements from 1 to n^2 in spiral order.

# Example
```
For example,
Given n = 3,
You should return the following matrix:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

# Analysis
题目要求按照旋转方式输出一个n*n的矩阵，这道题与`LeetCode54-Spiral Matrix`解法类似，按照数字递增的顺序依次向数组中对应位置填充数字1~n*n，填充的顺序按照四步从外到内一层一层进行。

# Solution
```
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> res(n,vector<int>(n,0));
        int count=1;
        int layer=(n+1)/2;
        int i,j;
        for(int k=0;k<layer;k++)
        {
            for(i=k,j=k;j<n-k;j++)
            {
                res[i][j]=count;
                count++;
            }
            for(i=k+1,j=n-1-k;i<n-k;i++)
            {
                res[i][j]=count;
                count++;
            }
            for(i=n-1-k,j=n-2-k;(n-1-k!=k)&&j>=k;j--)
            {
                res[i][j]=count;
                count++;
            }
            for(i=n-2-k,j=k;(n-1-k!=k)&&i>k;i--)
            {
                res[i][j]=count;
                count++;
            }
        }
        return res;
    }
};
```
