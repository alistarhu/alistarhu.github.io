---
layout:     post
title:      LeetCode 69. Sqrt(x)
subtitle:   
date:       2018-03-10
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 69. Sqrt(x) - Easy

# Description
Implement int sqrt(int x).

Compute and return the square root of x.

x is guaranteed to be a non-negative integer.

# Example
```
Example 1:

Input: 4
Output: 2
Example 2:

Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since we want to return an integer, the decimal part will be truncated.
```

# Analysis
这道题要求实现开方运算，原理是找到一个数a，使得a*a==x，普通的线性复杂度肯定不能满足要求，这里需要缩小搜索范围，**这里采用二分查找思想**

从1~x逐步折半查找。这里有两点需要注意：
- 采用`mid=left+(right-left)/2`计算中间值，为了防止`(left+right)/2`计算求和时溢出
- 由于这里开方要求输出是int，在开方不是整数的情况下，我们要去取res^2不超过x的res最大值，这里在每次更新左端值都将mid保存在res中，最后一次跟新的res即为所求

# Solution
```
class Solution {
public:
    int mySqrt(int x) {
        int left=1;
        int right=x;
        int res=0;
        while(left<=right)
        {
            // USE this rather than (left+right)/2 to overcome overflow of the sum
            int mid=left+(right-left)/2;
            if(mid==x/mid)
                return mid;
            else if(mid<x/mid)
            {
                res=mid;
                left=mid+1;
            }
            else
                right=mid-1;
        }
        return res;
    }
};
```
