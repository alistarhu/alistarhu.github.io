---
layout:     post
title:      LeetCode 38. Count and Say
subtitle:   
date:       2018-02-22
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 38. Count and Say - Easy

# Description
The count-and-say sequence is the sequence of integers with the first five terms as following:
```
1.     1
2.     11
3.     21
4.     1211
5.     111221
```
`1` is read off as `"one 1"` or `11`.

`11` is read off as `"two 1s"` or `21`.

`21` is read off as `"one 2, then one 1"` or `1211`.

Given an integer n, generate the nth term of the count-and-say sequence.

**Note:** Each term of the sequence of integers will be represented as a string.

# Example
```
Example 1:
Input: 1
Output: "1"

Example 2:
Input: 4
Output: "1211"
```

# Analysis
题目意思是：将人对于字符串计数并描述出来作为下一个字符串，从"1"开始一直循环下去，要求输出第n个序列。
- 第一个字符串是`1`，读作“一个1”，写成`11`，因此第二个字符串是第一个的结果`11`
- 第二个字符串`11`读作“两个1”，写成`21`
- 第三个字符串`21`读作“一个2一个1”，写成`1211`
- 第四个字符串`1211`读作“一个1一个2两个1”，写成`111221`,按照这种规律循环下去。。。

这道题其实是考察统计字符串中连续重复字符的个数，直接循环即可

# Solution
```
class Solution {
public:
    string countAndSay(int n) {
        string pre="1";
        string cur="";
        if(n==1)
            return "1";
        for(int i=2;i<=n;i++)
        {
            char ch,tmp;
            int ct=0;
            for(int j=0;j<pre.size();j++)
            {
                if(j==0)
                {
                    ch=pre[j];
                    ct=1;
                }
                else if(pre[j]!=pre[j-1])
                {
                    tmp='0'+ct;
                    cur=cur+tmp+ch;
                    ch=pre[j];
                    ct=1;
                }
                else
                    ct=ct+1;
            }
            tmp='0'+ct;
            cur=cur+tmp+ch;
            pre=cur;
            cur="";
        }
        return pre;
    }
};
```
