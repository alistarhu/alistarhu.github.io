---
layout:     post
title:      LeetCode 8. String to Integer (atoi)
subtitle:   
date:       2018-02-04
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 8. String to Integer (atoi) - Medium

# Description
Implement `atoi` to convert a string to an integer.

**Hint:** Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

**Notes:** It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

# Example
```

```

# Analysis
- 题目要求实现从字符串到数字的转换，有两点需要注意：
  - 需要对字符串开头的一串空格符进行剔除，如"      0123"
  - 需要对输入的数字是否溢出做判断

# Solution
```
class Solution {
public:
    int myAtoi(string str) {
        int sign=1;
        int i=0;
        // Skip the blank space
        while(i<str.size() && str[i]==' ')
            i++;
        if(str[i]=='-'||str[i]=='+')
        {
            if(str[i]=='-')
                sign=-1;
            i++;
        }
        int res=0;
        while(i<str.size() && str[i]>='0' && str[i]<='9')
        {
            // Deal with overflow
            if(res>INT_MAX/10 || (res==INT_MAX/10&&str[i]-'0'>INT_MAX%10))
                return sign==-1?INT_MIN:INT_MAX;
            res=res*10+str[i]-'0';
            i++;
        }
        return res*sign;
    }
};
```
