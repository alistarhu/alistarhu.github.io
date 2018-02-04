---
layout:     post
title:      LeetCode 7. Reverse Integer
subtitle:   
date:       2018-02-04
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 7. Reverse Integer - Easy

# Description
Given a 32-bit signed integer, reverse digits of an integer.
Note:

Assume we are dealing with an environment which could only hold integers within the 32-bit signed integer range. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

# Example
Example 1:
```
Input: 123
Output:  321
```
Example 2:
```
Input: -123
Output: -321
```
Example 3:
```
Input: 120
Output: 21
```

# Analysis
- 题目要求将一个int翻转后的结果输出，如果翻转后溢出则输出0.
- 重点是对于溢出的判断。由于输入是int，在翻转前后数据的位数保持一致，那么溢出可以分为两种情况：
  - 1、翻转后的数字的前n-1位>INT_MAX/10，即前n-1位数字引起溢出；
  - 2、最后一位发生溢出res*10+x%10>INT_MAX (程序中写成 INT_MAX-x%10<res*10)

# Solution
```
class Solution {
public:
    int reverse(int x) {
        int res=0;
        int flag=1;
        if(x<0)
            flag=-1;
        x=abs(x);
        while(x)
        {
            if(res>INT_MAX/10||INT_MAX-x%10<res*10)
                return 0;
            res=res*10+x%10;
            x=x/10;
        }
        return res*flag;
    }
};
```
