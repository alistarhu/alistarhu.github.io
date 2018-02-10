---
layout:     post
title:      LeetCode 12. Integer to Roman
subtitle:   
date:       2018-02-10
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 12. Integer to Roman - Medium

# Description
Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.

# Example
```

```

# Analysis
使用查表的方式，将个位、十位、百位、千位的所对应的罗马字母存在数组中，将各个位置上所对应的罗马字母拼接起来即可得到最终结果。

# Solution
```
class Solution {
public:
    string intToRoman(int num) {
        string M[] = {"", "M", "MM", "MMM"};
        string C[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        string X[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        string I[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
        string res;
        res=M[num/1000]+C[(num%1000)/100]+X[(num%100)/10]+I[num%10];
        return res;
    }
};
```
