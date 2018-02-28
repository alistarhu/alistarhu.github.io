---
layout:     post
title:      LeetCode 33. Search in Rotated Sorted Array
subtitle:   
date:       2018-02-20
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 33. Search in Rotated Sorted Array - Medium

# Description
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

# Example
```

```

# Analysis
题目要求在旋转数组(形如45678123)中查找特定数字，这里利用二分查找思想(时间复杂度O(nlgn))，根据mid和target所处的区间分为四种情况：
- 如果mid处于前部分，且target在left~mid之间，则更新right=mid-1
- 如果mid处于前部分，且target在mid的右侧，则更新left=mid+1
- 如果mid处于后部分，且target在mid~right之间，则更新left=mid+1
- 如果mid处于后部分，且target在mid左侧，则更新right=mid-1
注意if语句条件中的等号的设置！！！

# Solution
```
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int i=0;
        int j=nums.size()-1;
        while(i<=j)
        {
            int mid=(i+j)/2;
            if(nums[mid]==target)
                return mid;
            // If mid in the first part
            if(nums[mid]>=nums[i])
            {
                // target is in [i,mid]
                if(target>=nums[i]&&target<nums[mid])
                    j=mid-1;
                else
                    i=mid+1;
            }
            else    // mid in the second part
            {
                if(target<nums[i]&&target>nums[mid])
                    i=mid+1;
                else
                    j=mid-1;
            }
        }
        return -1;
    }
};
```
