---
layout:     post
title:      LeetCode 50. Pow(x, n)
subtitle:   
date:       2018-02-26
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 50. Pow(x, n) - Medium

# Description
Implement `pow(x, n)`.

# Example
```
Example 1:
Input: 2.00000, 10
Output: 1024.00000

Example 2:
Input: 2.10000, 3
Output: 9.26100
```

# Analysis
这道题要求实现一个数的n次幂，如果直接使用n次乘法运算求解，计算复杂度过高会超时。

这里采用折半的方法：x^n=x^(n/2)* x^(n/2)或x^n=x*x^(n/2)* x^(n/2)，这样逐层递归减少了乘法计算的次数，时间复杂度为O(log n)。

# Solution
```
class Solution {
public:
    double myPow(double x, int n) {
        if(n==0)
            return 1;
        if(n==INT_MIN)
        {
            x=x*x;
            n=n/2;
        }
        if(n<0)
        {
            n=abs(n);
            x=1/x;
        }
        double tmp=myPow(x,n/2);
        double res;
        if(n%2==0)
            res=tmp*tmp;
        else
            res=x*tmp*tmp;
        return res;
    }
};

/*
// 另外一种使用迭代计算的方法
public class Solution {
    public double MyPow(double x, int n) {
        double ans = 1;
        long absN = Math.Abs((long)n);
        while(absN > 0) {
            if((absN&1)==1) ans *= x;
            absN >>= 1;
            x *= x;
        }
        return n < 0 ?  1/ans : ans;
    }
}
*/
```
