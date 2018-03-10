---
layout:     post
title:      LeetCode 66. Plus One
subtitle:   
date:       2018-03-10
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 66. Plus One - Easy

# Description
Given a non-negative integer represented as a non-empty array of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.

# Example
```

```

# Analysis
这道题要求实现大数加法操作（加1操作）。从最低位（数组尾元素）向高位依次遍历，主要是对于进位的处理。

# Solution
```
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int over=1;
        for(int i=digits.size()-1;i>=0;i--)
        {
            int sum=digits[i]+over;
            digits[i]=sum%10;
            over=sum/10;
        }
        if(over==1)
            digits.insert(digits.begin(),1);
        return digits;
    }
};
```
