---
layout:     post
title:      LeetCode 56. Merge Intervals
subtitle:   
date:       2018-02-28
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 56. Merge Intervals - Medium

# Description
Given a collection of intervals, merge all overlapping intervals.

# Example
```
For example,
Given [1,3],[2,6],[8,10],[15,18],
return [1,6],[8,10],[15,18].
```

# Analysis
题目要求将给定的一系列区间进行合并。

具体做法：首先将区间段按照起始点顺序进行排序，然后将排序后的区间段从前往后进行合并，如果两个区间没有重叠，则将区间加入res中；如果区间存在重叠，则对区间end点进行修正。

# Solution
```
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
class Solution {
public:
    vector<Interval> merge(vector<Interval>& intervals) {
        vector<Interval> res;
        if(intervals.size()==0)
            return res;
        sort(intervals.begin(),intervals.end(),[](Interval a,Interval b){return a.start<b.start;});
        res.push_back(intervals[0]);
        for(auto it:intervals)
        {
            if(it.start>res.back().end)
                res.push_back(it);
            else if(it.end>res.back().end)
                res.back().end=it.end;
        }
        return res;
    }
};
```
