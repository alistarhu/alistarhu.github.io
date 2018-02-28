---
layout:     post
title:      LeetCode 58. Length of Last Word
subtitle:   
date:       2018-02-28
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 58. Length of Last Word - Easy

# Description
Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

**Note:** A word is defined as a character sequence consists of non-space characters only.

# Example
```
For example,
Input: "Hello World"
Output: 5
```

# Analysis
题目要求计算字符串中最后一个单词的长度。
- 由于单词之间是以空格来做分割的，使用循环依次扫描字符串中每个字符，依次统计每个单词的长度。
- 使用变量`start`记录每个单词的起始位置，一旦找到一个单词的起始，则进入一个循环直到遇到空格为止（表示一个单词结束了），同时记录下每个单词的长度，依次一个个单词的扫描，最后一次所求的单词长度即为所求。

# Solution
```
class Solution {
public:
    int lengthOfLastWord(string s) {
        int wordlen=0;
        int start=0;
        int i=0;
        while(i<s.size())
        {
            // Find the start idx of a word
            if(s[i]!=' ')
            {
                start=i;
                // Find the end idx of a word
                while(i<s.size()&&s[i]!=' ')
                    i++;
                wordlen=i-start;
            }
            else
                i++;
        }
        return wordlen;
    }
};
```
