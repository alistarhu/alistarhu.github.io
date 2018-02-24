---
layout:     post
title:      LeetCode 43. Multiply Strings
subtitle:   
date:       2018-02-24
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 43. Multiply Strings - Medium

# Description
Given two non-negative integers `num1` and `num2` represented as strings, return the product of `num1` and `num2`.

**Note:**
- The length of both `num1` and `num2` is < 110.
- Both `num1` and `num2` contains only digits `0-9`.
- Both `num1` and `num2` does not contain any leading zero.
- You must not use any built-in BigInteger library or convert the inputs to integer directly.

# Example
```

```

# Analysis
题目要求实现大数乘法，按照两个多位数相乘的原理可知：假设abcd*efg，最终的结果是1*g*abcd+10*f*abcd+100*e*abcd，也就是被乘数的每一位数与乘数依次相乘，然后将相乘的结果对应的相加起来，最终的相乘结果最多有m+n位数（m为乘数的位数，n为被乘数的位数）。
```
   xxxx
*   xxx
--------
   xxxx
+ xxxx
--------
  XXXXX  
```
程序中实现方法：**新建一个长度为m+n的数组，数组中的每一元素对应最终乘积结果的每一位**，使用两个for循环实现每个位上的被乘数与每个位上的乘数的乘积运算，将运算结果累加到它所属的数位上，同时注意进位的处理。此外还需要对最终结果中开头的0进行剔除操作。

# Solution
```
class Solution {
public:
    string multiply(string num1, string num2) {

        int m=num1.size();
        int n=num2.size();
        vector<int> sum(m+n,0);
        string res="";
        // Calculate product
        for(int i=n-1;i>=0;i--)
        {
            int carry=0;
            for(int j=m-1;j>=0;j--)
            {
                int tmp=(num1[j]-'0')*(num2[i]-'0')+sum[i+j+1]+carry;
                sum[i+j+1]=tmp%10;
                carry=tmp/10;
            }
            if(carry!=0)
                sum[i]+=carry;
        }
        // Generate result    
        int flag=0;
        for(int i=0;i<m+n;i++)
        {
            // Filter the leading zero case "000123"
            if(flag==0)
            {
                if(sum[i]==0)
                    continue;
                else
                    flag=1;
            }
            char ch=sum[i]+'0';
            res+=ch;
        }
        if(res.size()==0)
            return "0";
        else
            return res;
    }
};
```
