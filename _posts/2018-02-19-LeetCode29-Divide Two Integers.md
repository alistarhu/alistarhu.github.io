---
layout:     post
title:      29. Divide Two Integers
subtitle:   
date:       2018-02-19
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 29. Divide Two Integers - Medium

# Description
Divide two integers without using multiplication, division and mod operator.

If it is overflow, return MAX_INT.

# Example
```

```

# Analysis
- 题目要求在不适用乘除操作的情况下实现除法操作，因此我们可用的操作只剩下了减法和位运算两种计算。
- 一种最直观的方法式使用除数一直减去被除数，直至除数小于被除数位置，减的次数即为除法运算的结果。这种方法的复杂度为O(n)
- 这里对O(n)的方法进行优化，假设:a/b=c,**c可以写成2的幂次的形式c=k1*2^n+k2*2^(n-1)+....+kn**，这样时间复杂度由原来的O(n)变为了 **O(logn)**

# Solution
```
class Solution {
public:
    int divide(int dividend, int divisor) {
        int flag=((dividend < 0) ^ (divisor < 0)) ? -1 : 1;;
        // Overflow
        if((divisor==0)||(dividend==INT_MIN&&divisor==-1))
            return INT_MAX;
        long long dvd = labs(dividend);
        long long dvs = labs(divisor);
        int res = 0;
        while (dvd >= dvs)
        {
            long long temp = dvs, multiple = 1;
            while (dvd >= (temp << 1))
            {
                temp <<= 1;
                multiple <<= 1;
            }
            dvd -= temp;
            res += multiple;
        }
        return res*flag;
    }
};
```
