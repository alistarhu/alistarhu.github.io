---
layout:     post
title:      LeetCode 1. Two Sum
subtitle:   
date:       2018-01-23
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# LeetCode 1.Two Sum - Easy 

# Description 
Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

# Example
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

# Analysis
- 题目要求从一个数组中寻找和为给定值target的两个数。
- 解法一：最容易想到的一种方法就是暴力搜索，寻找两个数可以使用双重循环进行搜索，复杂度O(n^2)
- 解法二：可以构建一个hashmap，构建<元素值，下标>的键值对。每次来一个元素，先检查与该元素相配对的数是否在hashmap中，如果不存在，则将该元素添加到hashmap中；否则，说明已找到，直接返回结果。这样只需要遍历一遍数组即可。复杂度O(n)。

# Solution
```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> map;
        vector<int> res;
        for(int i=0;i<nums.size();i++)
        {
            // the paired number is found in map, return the result
            if(map.find(target-nums[i])!=map.end())
            {
                res.push_back(map[target-nums[i]]);
                res.push_back(i);
                return res;
            }
            // not find the paired number, put it in to map
            map.insert({nums[i],i});
        }
    }
};
```
