---
layout:     post
title:      LeetCode 54. Spiral Matrix
subtitle:   
date:       2018-02-26
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 54. Spiral Matrix - Medium

# Description
Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

# Example
```
For example,
Given the following matrix:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
You should return [1,2,3,6,9,8,7,4,5].
```

# Analysis
这道题要求将数组按照顺时针旋转的顺序由内向外打印出来。

这里我们采用由外向内一层层打印，每一层我们分为上方从左向右、右边的从上到下、下方的从右向左、左边的从下向上四步。特别需要注意最后两步，当矩阵行或是列为奇数时，最内层只有横着的一排，需要加限制条件`m-1-k!=k`和`n-1-k!=k`防止反方向（最后两步）将数组元素重复打印了。

# Solution
```
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int m=matrix.size();
        vector<int> res;
        if(m==0)
            return res;
        int n=matrix[0].size();
        int layer=(min(m,n)+1)/2;
        int i,j;

        for(int k=0;k<layer;k++)
        {
            for(i=k,j=k;j<n-k;j++)
                res.push_back(matrix[i][j]);
            for(i=k+1,j=n-1-k;i<m-k;i++)
                res.push_back(matrix[i][j]);
            for(i=m-1-k,j=n-2-k;(m-1-k!=k)&&j>=k;j--)
                res.push_back(matrix[i][j]);
            for(i=m-2-k,j=k;(n-1-k!=k)&&i>k;i--)
                res.push_back(matrix[i][j]);
        }
        return res;
    }
};
```
