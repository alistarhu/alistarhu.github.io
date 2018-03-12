---
layout:     post
title:      LeetCode 73. Set Matrix Zeroes
subtitle:   
date:       2018-03-12
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 73. Set Matrix Zeroes - Medium

# Description
Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.

# Example
```

```

# Analysis
这道题要求将数组中值为0的元素所在的行和列都填充上0.

思路：
- 利用第一行和第一列作为标志位，扫描整个数组(1~rowNum) * (1~colNum)，如果`(i,j)`为0，那么则需要将`a[0][j]`和`a[i][0]`表示第i行和第j列都需要设为0。这样在第二表扫描数组时，根据`a[0][j]`和`a[i][0]`是否为0，对`a[i][j]`的值进行设置。
- 这里利用第一列和第一行作为标志位，那如果第一列或第一行原本就有0元素呢？因此这里我们需要需要设置两个标志位，来表征第一行或第一列本身就含有0元素。因为如果第一行（第一列）中本身就含有0元素，我们不仅需要将相应的列设为0，同时还需要将第一行一整行整体设为0。

# Solution
```
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        bool rowFlag=false;
        bool colFlag=false;
        int rowNum=matrix.size();
        int colNum=matrix[0].size();
        // Cheak first row
        for(int j=0;j<colNum;j++)
            if(matrix[0][j]==0)    // first row has real zero num, we should set the holl row to zeros
                rowFlag=true;   
        // Cheak first col
        for(int i=0;i<rowNum;i++)
            if(matrix[i][0]==0)    // first col has real zero num, we should set the holl col to zeros
                colFlag=true;
        for(int i=1;i<rowNum;i++)
        {
            for(int j=1;j<colNum;j++)
            {
                if(matrix[i][j]==0)
                {
                    matrix[i][0]=0;
                    matrix[0][j]=0;
                }
            }
        }

        // Set the zeros
        for(int i=1;i<rowNum;i++)
        {
            for(int j=1;j<colNum;j++)
            {
                if(matrix[i][0]==0||matrix[0][j]==0)
                    matrix[i][j]=0;
            }
        }
        for(int j=0;j<colNum;j++)
            if(rowFlag)
                matrix[0][j]=0;
        for(int i=0;i<rowNum;i++)
            if(colFlag)
                matrix[i][0]=0;
    }
};
```
