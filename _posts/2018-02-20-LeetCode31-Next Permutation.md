---
layout:     post
title:      31. Next Permutation
subtitle:   
date:       2018-02-20
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 31. Next Permutation - Medium

# Description
Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place, do not allocate extra memory.

# Example
```
Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```

# Analysis
题目要求计算下一组数字的下一个排列（按照递增方向的下一个）。

这里以`24689`这几个数的排列举例。
- `98642`的下一个排列为`24689`，因为数字已经达到最大了，下一个全排列是最小的数
- `24986`的下一个排列为`26489`，在计算`24986`下一个排列的过程：后三个数字`6` `8` `9`已经是他们最大的排列数`986`(**降序排列**)，因此比`24986`大的下一排列数必须在倒数第四位数`4`上做改变(**最靠近右侧的先升后降的分隔点**)，我们需要在后三个数中挑一个 **稍稍大于**`4`的数`6`去与它交换，然后将新的后三位数字按照升序排列`489`即可，也就得到了最终的结果`26489`
- 更一般的例子`24869`的下一个排列为`24896`，按照前一个例子的方法：我们的分隔点位于数字`6`的位置上，前一个例子中的三个数字对应到这里只有一个数字`6`

程序具体实现步骤：
- step1:从后往前搜索，找到第一个满足`nums[i] < nums[i + 1]`的坐标，我们把它记作k。（我们所求的下一个排列数，在k这个位置上的数需要比原先稍微大一点点）
- step2:从`k+1~nums.size()-1`,找一个刚刚比nums[k]大的数。由于`k+1~nums.size()-1`已经是非升序排列，我们直接从后往前搜索第一次比`nums[k]`大的数即为所求，它的坐标记为l
- step3:将`nums[k]`和`nums[l]`进行交换，并将`k+1~nums.size()-1`的数字按照升序排列即可得到最终答案

# Solution
```
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
      // Step1: find k
      int k = -1;
    	for (int i = nums.size() - 2; i >= 0; i--)
      {
    		if (nums[i] < nums[i + 1])
        {
    			k = i;
    			break;
    		}
    	}
    	if (k == -1) {
    	    reverse(nums.begin(), nums.end());
    	    return;
    	}
    	int l = -1;
    	for (int i = nums.size() - 1; i > k; i--) {
    		if (nums[i] > nums[k]) {
    			l = i;
    			break;
    		}
    	}
    	swap(nums[k], nums[l]);
    	reverse(nums.begin() + k + 1, nums.end());
    }
};
```
