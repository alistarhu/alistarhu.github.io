---
layout:     post
title:      LeetCode 22. Generate Parentheses
subtitle:   
date:       2018-02-18
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 22. Generate Parentheses - Medium

# Description
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

# Example
```
For example, given n = 3, a solution set is:
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

# Analysis
- 题目要求生成给定数目的匹配括号对，这里使用递归的方式求解
- left、right表示剩余可添加的左右括号数。每次添加括号有两种选择（对应dfs函数中的后两个if语句）:如果左括号数目还有剩余，则可以选择添加左括号，将左括号数减一递归进入下轮；如果 **左括号数<右括号数**，则可以选择添加右括号（因为 **如果左=右，此时继续选择添加右括号则会造成不匹配现象**，如：(....))）。如果left=right=0，则表示找到了一个解，将结果保存下来停止递归操作。

# Solution
```
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> res;
        string s;
        dfs(n,n,s,res);
        return res;
    }

    void dfs(int left,int right,string s,vector<string> &res)
    {
        if(left==0&&right==0)
        {
            res.push_back(s);
            return;
        }
        if(left>0)
            dfs(left-1,right,s+"(",res);
        if(right>0&&left<right)
            dfs(left,right-1,s+")",res);
    }
};
```
