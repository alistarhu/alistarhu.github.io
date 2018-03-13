---
layout:     post
title:      LeetCode 75. Sort Colors
subtitle:   
date:       2018-03-13
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 75. Sort Colors - Medium

# Description
Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note: You are not suppose to use the library's sort function for this problem.

# Example
```

```

# Analysis
这道题要求将一个包含数字：0、1、2的数组按照顺序排序。

这里采用 **只扫描一次数组** 的方法，具体做法：假设前`i-1`个元素已经按照`001122`的形式排好序了，并且将已排好序`0~i-1`数组中最后一个0、最后一个1、最后一个2的坐标记作idx0、idx1、idx2。数组当前位置`i`的元素有三种可能
- 如果`nums[i]==2`，则将`nums[++idx2]=2`,其实也就是将idx2做了更新；
- 如果`nums[i]==1`，则需要将这个1插到相应位置上，也就是首先将前面排好序数组中值为2的元素往后挪一个位置，然后在已经排好序数组中1元素后面插入元素1即可，即`nums[++idx2]=2;nums[++idx1]=1`;
- 如果`nums[i]==0`，则需要将排好序数组中的1和2整体后移一位（由于元素相同，其实只涉及两次拷贝赋值操作），然后在0的后面插入一个0即可，`nums[++idx2]=2;nums[++idx1]=1;nums[++idx0]=0;`

# Solution
```
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int idx0=-1,idx1=-1,idx2=-1;
        for(int i=0;i<nums.size();i++)
        {
            if(nums[i]==2)
            {
                nums[idx2+1]=2;
                idx2++;
            }
            else if(nums[i]==1)
            {
                nums[idx2+1]=2;
                idx2++;
                nums[idx1+1]=1;
                idx1++;
            }
            else
            {
                nums[idx2+1]=2;
                idx2++;
                nums[idx1+1]=1;
                idx1++;
                nums[idx0+1]=0;
                idx0++;
            }
        }
    }
};
```
