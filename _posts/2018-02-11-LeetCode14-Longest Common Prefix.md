---
layout:     post
title:      LeetCode 14. Longest Common Prefix
subtitle:   
date:       2018-02-11
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 14. Longest Common Prefix - Easy

# Description
Write a function to find the longest common prefix string amongst an array of strings.

# Example
```

```

# Analysis
求最长公共前缀。思路：首先计算前两个字符串的公共前缀，然后将所得的公共前缀与下一个字符串求公共前缀从而得到新的前缀，依次循环下去。。。

# Solution
```
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.size()==0)
            return "";
        string res=strs[0];
        for(int i=1;i<strs.size();i++)
        {
            string cur_str=strs[i];
            string prefix=res;
            // calculate the prefix string between 'cur_str' and 'prefix' and store in res
            res="";
            for(int j=0;j<min(cur_str.size(),prefix.size());j++)
            {
                if(cur_str[j]==prefix[j])
                    res=res+cur_str[j];
                else
                    break;
            }
        }
        return res;
    }
};
```
