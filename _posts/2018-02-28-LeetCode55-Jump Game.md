---
layout:     post
title:      LeetCode 55. Jump Game
subtitle:   
date:       2018-02-28
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 55. Jump Game - Medium

# Description
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

# Example
```
For example:
A = [2,3,1,1,4], return true.
A = [3,2,1,0,4], return false.
```

# Analysis
题目中给定一个数组表示每个位置上可移动的步数，求从左端能否移动到右端。

具体实现方法：采用一个变量`maxIdx`记录每次运动所能到达的最远距离，依次遍历数组，如果`i>maxIdx`说明根本到不了i这个位置，也就不可能从i这个位置继续往后走从而更新maxIdx；如果`i<=maxIdx`，表明可以从当前点先后走，根据nums[i]的值计算出从当前位置所能向后走的最远距离，更新maxIdx，由此循环下去。这里加了一个提前终止条件`maxIdx<nums.size()`因为maxIdx==nums.size()-1时，说明已经到达了最右端，可以直接返回结果不需要继续向后迭代了。

# Solution
```
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int maxIdx=0;
        for(int i=0;i<nums.size()&&i<=maxIdx&&maxIdx<nums.size();i++)
            if(nums[i]+i>maxIdx)
                maxIdx=nums[i]+i;
        return maxIdx>=nums.size()-1;
    }
};
```
