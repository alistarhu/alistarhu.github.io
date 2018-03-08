---
layout:     post
title:      LeetCode 60. Permutation Sequence
subtitle:   
date:       2018-03-08
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 60. Permutation Sequence - Medium

# Description
The set `[1,2,3,…,n]` contains a total of n! unique permutations.

By listing and labeling all of the permutations in order,
We get the following sequence (ie, for n = 3):
'''
1  "123"
2  "132"
3  "213"
4  "231"
5  "312"
6  "321"
'''
Given n and k, return the kth permutation sequence.

**Note:** Given n will be between 1 and 9 inclusive.

# Example
```

```

# Analysis
题目要求计算n个数的第k个全排列，这里根据全排列的排列规律进行求解。

规律：n个数共有n!种全排列，根据第一个元素的不同可将全排列分为n组，每组中包含(n-1)!种全排列，即：第一组中是由2~n组成的全排列，第二组中是由1、3~n组成的全排列。k/(n-1)!代表属于哪个区间（区间号），k%(n-1)!表示在该区间内的第多少号。因此我们可以根据k值的大小确定第k个全排列所属的区间，依次确定每一个位置上的元素，逐渐缩小搜索的范围。这里采用一个数组`tab`充当一个集合的作用，用于标记哪些元素已经被使用了、哪些元素当前可用。

# Solution
```
class Solution {
public:
    string getPermutation(int n, int k) {
        k = k - 1;
        int jie = 1;
        for (int i = 2; i <= n; i++)
            jie = jie*i;
        vector<int> tab(n, 0);
        string s = "";
        for (int i = 0; i<n; i++)
        {
            jie = jie / (n - i);
            int idx = k / jie;
            int count = 0;
            int j=0;
            char ch;
            while (j < n)
            {
                if (tab[j] == 0)
                    count++;
                if (count == idx + 1)
                {
                    ch = '0' + j+1;
                    tab[j] = 1;
                    break;
                }
                j++;
            }
            s = s + ch;
            k = k%jie;
        }
        return s;
    }
};
```
