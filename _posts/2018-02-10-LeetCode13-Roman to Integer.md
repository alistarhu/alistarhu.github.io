---
layout:     post
title:      LeetCode 13. Roman to Integer
subtitle:   
date:       2018-02-10
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 13. Roman to Integer - Easy

# Description
Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

# Example
```

```

# Analysis
- 根据罗马数字构成规律：如果前<后，表示(后-前)的数字（被减的数字只能出现一次）;其余情况都是相互叠加关系。
- 遍历罗马字符，将当前字符所对应的数字加到结果中，**如果发现当前字符所对应的数字小于前一个字符（说明前一个字符代表相减的关系），由于之前遍历到它的时候已经加了一次，所以需要减去前个字符所对应值的2倍。**

# Solution
```
class Solution {
public:
    int romanToInt(string s) {
        map<char,int> tab({{'I',1},{'V',5},{'X',10},{'L',50},{'C',100},{'D',500},{'M',1000}});
        int res=tab[s[0]];
        for(int i=1;i<s.size();i++)
        {
            res=res+tab[s[i]];
            if(tab[s[i-1]]<tab[s[i]])
                res=res-2*tab[s[i-1]];
        }
        return res;
    }
};
```
