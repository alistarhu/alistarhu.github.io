---
layout:     post
title:      LeetCode 48. Rotate Image
subtitle:   
date:       2018-02-25
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 48. Rotate Image - Medium

# Description
You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

**Note:** You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

# Example
```
Example 1:
Given input matrix =
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],
rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]

Example 2:
Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
],
rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

# Analysis
题目要求将一个二维数组方阵顺时针旋转90度，并且不能开辟额外的数组空间，那么则要求在原始数组上的进行数字交换操作。

有一种两步法：第一步将数组进行上下翻转，之后按照主对角线翻转，两步操作之后就达到了原始数组顺时针旋转90度的效果
```
 * clockwise rotate
 * first reverse up to down, then swap the symmetry
 * 1 2 3     7 8 9     7 4 1
 * 4 5 6  => 4 5 6  => 8 5 2
 * 7 8 9     1 2 3     9 6 3
```

# Solution
```
// Solution 1: Two step reverse
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        // reverse up to down
        reverse(matrix.begin(),matrix.end());
        // reverse up to down
        for(int i=0;i<matrix.size();i++)
            for(int j=i+1;j<matrix[i].size();j++)
                swap(matrix[i][j],matrix[j][i]);
    }
};

// Solution2:
class Solution {
public:
    void rotate(vector<vector<int> > &matrix) {
        int n = matrix.size();
        for (int i = 0; i < n / 2; ++i) {
            for (int j = i; j < n - 1 - i; ++j) {
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[n - 1 - j][i];
                matrix[n - 1 - j][i] = matrix[n - 1 - i][n - 1 - j];
                matrix[n - 1 - i][n - 1 - j] = matrix[j][n - 1 - i];
                matrix[j][n - 1 - i] = tmp;
            }
        }
    }
};
```
