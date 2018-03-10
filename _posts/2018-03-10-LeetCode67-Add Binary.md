---
layout:     post
title:      LeetCode 67. Add Binary
subtitle:   
date:       2018-03-10
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 67. Add Binary - Easy

# Description
Given two binary strings, return their sum (also a binary string).

# Example
```
For example,
a = "11"
b = "1"
Return "100".
```

# Analysis
这道题要求实现两个二进制数加法运算，这里还是采用从最低位向最高位依次逐位累加（含进位）的方式，使用一个字符数组用于计算累加的结果，注意数组的空间等于`len=max(len1,len2)+1`这里加1是为了防止有进位因此需要多开辟出一个空位出来。

# Solution
```
class Solution {
public:
    string addBinary(string a, string b) {
        int len1=a.size();
        int len2=b.size();
        int len=max(len1,len2)+1;
        vector<char> tmp(len,'0');
        int i=len1-1;
        int j=len2-1;
        int k=len-1;
        int over=0;
        while(i>=0||j>=0)
        {
            int sum=over;
            if(i>=0)
                sum=sum+a[i--]-'0';
            if(j>=0)
                sum=sum+b[j--]-'0';
            tmp[k]=sum%2+'0';
            over=sum/2;
            k--;
        }
        if(over==1)
            tmp[k]=over+'0';
        else
            k=1;
        string res="";
        while(k<len)
        {
            res=res+tmp[k];
            k++;
        }
        return res;
    }
};
```
