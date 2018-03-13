---
layout:     post
title:      LeetCode 74. Search a 2D Matrix
subtitle:   
date:       2018-03-13
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 74. Search a 2D Matrix - Medium

# Description
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:
- Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.

# Example
```
Consider the following matrix:
[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
Given target = 3, return true.
```

# Analysis
这道题要求在一个二维数组中查找特定元素，由于数组从左到右是有序的，并且下面行元素的值比上面行元素值要大，因此可以将整个数组按行拼接拉成一个一维数组，然后采用二分查找对数组元素进行搜索即可。

# Solution
```
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m=matrix.size();
        if(m==0)
            return false;
        int n=matrix[0].size();
        int left=0;
        int right=m*n-1;
        while(left<=right)
        {
            int mid=(left+right)/2;
            if(matrix[mid/n][mid%n]==target)
                return true;
            else if(matrix[mid/n][mid%n]>target)
                right=mid-1;
            else
                left=mid+1;
        }
        return false;
    }
};
```
