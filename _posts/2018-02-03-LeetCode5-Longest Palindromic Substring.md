---
layout:     post
title:      LeetCode 5. Longest Palindromic Substring
subtitle:   
date:       2018-02-03
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 5. Longest Palindromic Substring - Medium

# Description
Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

# Example
```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.

Input: "cbbd"
Output: "bb"
```

# Analysis
- 采用从中间向两边搜索的方式，时间复杂度O(n^2)
- 外循环依次遍历每个字符，以每个字符作为中心元素；内循环（ 函数subIsPalindrome（））由中心向两边扩散，用于查找以当前字符为中心的最长回文子串
- 其中中心元素分为两种情况：奇数aba、偶数abba

# Solution
```
class Solution {
public:
    int start=0;
    int end=0;
    string longestPalindrome(string s) {
        int len=s.size();
        if(len<2)
            return s;
        for(int i=0;i<len-1;i++)
        {
            subIsPalindrome(s,i,i); // the longest palindrome len is odd
            subIsPalindrome(s,i,i+1);// the longest palindrome len is even
        }
        return s.substr(start,end-start+1);
    }

    void subIsPalindrome(string s,int m,int n){
        while(m>=0 && n<s.size() && s[m]==s[n])
        {
            m--;
            n++;
        }
        if((end-start)<(n-m-2))
        {
            start=m+1;
            end=n-1;
        }
    }
};
```
