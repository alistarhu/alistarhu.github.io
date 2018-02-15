---
layout:     post
title:      LeetCode 17. Letter Combinations of a Phone Number
subtitle:   
date:       2018-02-15
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 17. Letter Combinations of a Phone Number - Medium

# Description
Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.

![telephonekeypad](https://raw.githubusercontent.com/AlistarHu/alistarhu.github.io/master/img/Leetcode17_Telephonekeypad.png)

**Note:** Although the above answer is in lexicographical order, your answer could be in any order you want.

# Example
```
Input:Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

# Analysis
采用迭代的方式求排列数

# Solution
```
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        string charmap[]={"0","1","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
        vector<string> res;
        if(digits.size()==0)
            return res;
        res.push_back("");
        for(int i=0;i<digits.size();i++)
        {
            string cur_str=charmap[digits[i]-'0'];
            vector<string> tmp_res;
            for(int j=0;j<res.size();j++)
            {
                for(int k=0;k<cur_str.size();k++)
                    tmp_res.push_back(res[j]+cur_str[k]);
            }
            res=tmp_res;
        }
        return res;
    }
};
```
