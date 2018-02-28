---
layout:     post
title:      LeetCode 28. Implement strStr()
subtitle:   
date:       2018-02-19
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 28. Implement strStr() - Easy

# Description
Implement `strStr()`.

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

# Example
```
Example 1:
Input: haystack = "hello", needle = "ll"
Output: 2

Example 2:
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

# Analysis
题目要求实现查找一个字符串在另一个字符串中首次出现的位置，直接使用双重循环即可。

# Solution
```
class Solution {
public:
    int strStr(string haystack, string needle) {
        if(haystack.size()<needle.size())
            return -1;
        for(int i=0;i<haystack.size()-needle.size()+1;i++)
        {
            int j;
            for(j=0;j<needle.size();j++)
            {
                if(haystack[i+j]!=needle[j])
                    break;
            }
            if(j==needle.size())
                return i;
        }
        return -1;
    }
};
```
