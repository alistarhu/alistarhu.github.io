---
layout:     post
title:      LeetCode 6. ZigZag Conversion
subtitle:   
date:       2018-02-04
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 6. ZigZag Conversion - Medium

# Description
The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
```
P   A   H   N
A P L S I I G
Y   I   R
```
And then read line by line: `"PAHNAPLSIIGYIR"`
Write the code that will take a string and make this conversion given a number of rows:
```
string convert(string text, int nRows);
```
`convert("PAYPALISHIRING", 3)` should return `"PAHNAPLSIIGYIR"`.

# Example
```
Input: "PAYPALISHIRING"
Output: "PAHNAPLSIIGYIR"
```

# Analysis
- 题目要求按照“之”字形对字符串进行输出，属于找规律的题
```
0       8
1     7 9        ......
2   6   10     14
3 5     11  13
4       12
```
- 以4行举例：它们同一行相邻元素之间索引的间隔是有规律的，如：i=1，它的下一个数字idx是7(gap1=(numRows-1-i)=6)，7的下一个数字idx是9(gap2=2*i)。gap1我们定义为先下后上（类似“v”）间隔，gap2我们定义为先上后下（类似“^”）间隔。
- 每一行的首个元素在字符串中的索引是i（行号），每一行之后的元素（在字符串中）索引都是在前一个元素索引基础上交替叠加gap1、gap2得到的。

# Solution
```
class Solution {
public:
    string convert(string s, int numRows) {
        string res="";
        if(numRows==1)//!!!!!
            return s;
        for(int i=0;i<numRows;i++)
        {
            int idx=i;
            if(idx<s.size())
                res+=s[idx];
            int gap1=2*(numRows-1-i);
            int gap2=2*i;
            while(1)
            {
                idx+=gap1;
                if(idx>=s.size())
                    break;
                if(gap1)    // ignore the last row(gap1==0)
                    res+=s[idx];

                idx+=gap2;
                if(idx>=s.size())
                    break;
                if(gap2)    // ignore the first row(gap2==0)
                    res+=s[idx];
            }
        }
        return res;
    }
};
```
