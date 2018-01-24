---
layout:     post
title:      LeetCode 3. Longest Substring Without Repeating Characters
subtitle:   
date:       2018-01-24
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 3. Longest Substring Without Repeating Characters - Medium

# Description
Given a string, find the length of the longest substring without repeating characters.

# Example
```
Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

# Analysis
- 题目需要求字符串的最长公共子串（要求连续）。
- 应用动态规划思想，需要建立一个字典用于记录每个字符**上一次在字符串出现的位置**。
- 依次遍历字符串中的每个字符，如果字符是第一次出现（字典中没有），则将他插入字典；如果字典中存在该字符，则start需要更新为上次字符出现位置+1（因为序列中不允许重复元素，到当前字符为止的最长序列：map[ch]+1~ch）,同时还需要更新字典中字符的位置信息。
- 注意：**start=max(m[s[i]],start);** start需要更新为两个之中最靠右的，因为会出现 abXXXXXXba 的情况

# Solution
```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        map<char,int> m;
        int start=-1;
        int maxLen=0;
        for(int i=0;i<s.size();i++)
        {
            if(m.find(s[i])!=m.end())
                start=max(m[s[i]],start);
            m[s[i]]=i;
            maxLen=max(maxLen,i-start);
        }
        return maxLen;
    }
};
```
