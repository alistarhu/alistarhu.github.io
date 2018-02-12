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
        // scan each char of the first string
        for(int i=0;i<strs[0].size();i++)
        {
            // compare with other string of the idx=i
            for(int j=1;j<strs.size();j++)
            {
                if(strs[j].size()==i||strs[j][i]!=strs[0][i])
                    return strs[0].substr(0,i);
            }
        }
        return strs[0];
    }
};
```
