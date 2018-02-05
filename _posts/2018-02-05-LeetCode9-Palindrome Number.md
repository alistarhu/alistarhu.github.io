---
layout:     post
title:      LeetCode 9. Palindrome Number
subtitle:   
date:       2018-02-05
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 9. Palindrome Number - Easy

# Description
Determine whether an integer is a palindrome. Do this without extra space.

# Example
```

```

# Analysis
- 题目要求判断一个数是否是回文数，不能使用额外的空间。
- 这里采用数字翻转输出的思想，利用 **回文数中前一半和翻转后的后一半相等的特性** 进行回文数判断。

# Solution
```
class Solution {
public:
    bool isPalindrome(int x) {
        if (x<0 || (x!=0 && x%10==0)) //!!!!
            return false;
        int sub_num=0;
        while(x>sub_num)
        {
            sub_num=sub_num*10+x%10;
            x=x/10;
        }
        return (x==sub_num||x==sub_num/10);
    }
};
```
