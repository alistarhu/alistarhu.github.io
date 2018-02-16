---
layout:     post
title:      LeetCode 20. Valid Parentheses
subtitle:   
date:       2018-02-16
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 20. Valid Parentheses

# Description
Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

The brackets must close in the correct order, `"()"` and `"()[]{}"` are all valid but `"(]"` and `"([)]"` are not.

# Example
```

```

# Analysis
括号匹配问题，思路：括号匹配属于一种就近匹配原则，每次读入一个左括号则将其对应的右括号压入栈中（**栈中存放的是与左括号相匹配的右括号序列**）；如果读取的是右括号，则与栈顶的括号作比较，如果一致则说明左右括号相匹配，否则不匹配。

# Solution
```
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        for(char& c:s)
        {
            // Store the opposite char in stack
            if(c=='(')
                st.push(')');
            else if(c=='{')
                st.push('}');
            else if(c=='[')
                st.push(']');
            // Compare if is the right one
            else
            {
                if(st.empty()||st.top()!=c)
                    return false;
                else
                    st.pop();
            }
        }
        return st.empty();
    }
};
```
