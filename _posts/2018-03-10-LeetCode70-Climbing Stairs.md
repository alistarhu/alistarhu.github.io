---
layout:     post
title:      LeetCode 70. Climbing Stairs
subtitle:   
date:       2018-03-10
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 70. Climbing Stairs - Easy

# Description
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

# Example
```
Example 1:

Input: 2
Output:  2
Explanation:  There are two ways to climb to the top.

1. 1 step + 1 step
2. 2 steps
Example 2:

Input: 3
Output:  3
Explanation:  There are three ways to climb to the top.

1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

# Analysis
这道题是爬楼梯问题，每次可以选择走一阶或是二阶，问爬上一个n阶楼梯共有多少种方法。

这道题使用动态规划思想，每一次移动共有两种选择：爬一阶或是爬两阶，则有关系式`dp[n]=dp[n-1]+dp[n-2]`，dp[n]表示爬n阶楼梯的方法数，第一步如果选择爬1阶，那么爬完剩下的n-1阶共有dp[n-1]种方法；如果第一步选择爬2阶，那么爬完剩下的n-2阶共有dp[n-2]种方法。两种选择综合起来，爬n阶楼梯的方法数共有dp[n-1]+dp[n-2]。这里使用循环的方式从前往后迭代计算，dp[n]即为所求。

# Solution
```
class Solution {
public:
    int climbStairs(int n) {
        vector<int> res(n,0);
        if(n==1)
            return 1;
        else if(n==2)
            return 2;
        res[0]=1;
        res[1]=2;
        for(int i=2;i<n;i++)
            res[i]=res[i-1]+res[i-2];
        return res[n-1];
    }
};
```
