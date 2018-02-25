---
layout:     post
title:      LeetCode 49. Group Anagrams
subtitle:   
date:       2018-02-25
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 49. Group Anagrams - Medium

# Description
Given an array of strings, group anagrams together.

# Example
```
For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"],
Return:
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

# Analysis
这道题让我们在给定的字符串集中找出所有的错位词，错位词就是两个字符串中字母出现的次数都一样，只是位置不同。

由于错位词按照字母顺序重排后可以得到相同的字符串，所以可以将重新排序后的字符串作为key，将字符串保存到对应key的数组中。最后再将字典中的结果进行综合得到最终result。

# Solution
```
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        map<string,vector<string>> map;
        for(string str:strs)
        {
            string tmp=str;
            sort(tmp.begin(),tmp.end());
            map[tmp].push_back(str);
        }
        vector<vector<string>> res;
        for(auto it=map.begin();it!=map.end();it++)
            res.push_back(it->second);
        return res;
    }
};
```
