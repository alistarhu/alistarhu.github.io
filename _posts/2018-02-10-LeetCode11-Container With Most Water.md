---
layout:     post
title:      LeetCode 11. Container With Most Water
subtitle:   
date:       2018-02-10
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 11. Container With Most Water - Medium

# Description
Given n non-negative integers *a1, a2, ..., an,* where each represents a point at coordinate *(i, ai). n* vertical lines are drawn such that the two endpoints of line i is at *(i, ai)* and *(i, 0)*. Find two lines, which together with x-axis forms a container, such that the container contains the most water.

# Example
```

```

# Analysis
如果直接采用暴力搜索方式，复杂度O(n^2)。其实在搜索可行解时进行了许多不必要的计算，下面介绍一种优化过后的方法，时间复杂度O(n)。

以n=6为例，横行为起始，纵行为终止坐标，共有C<sup>2</sup><sub>n</sub>=15种。
```
  1 2 3 4 5 6
1 x
2 x x
3 x x x
4 x x x x
5 x x x x x
6 x x x x x x
```
这里采用由两边向中间搜索的方式（宽度越宽或是高度越高，两种情况都有可能是所寻找的最优解）。

第一次计算*(1,6)* 用`o`表示 ,如果左边线比右边线矮（即height[1]<height[6]），则*(1,2)、(1,3)、(1,4)、(1,5)* 都不可能比*(1,6)* 更优（水池的高度以矮的为基准，盛水量与宽度有关，宽度越小盛水越少），可以将这4个解用`-------`直接划去不用计算（横向划去），此处去掉了n-2个解。**相当于左边指针右移一位，以2作为左边起始点**（同理，如果左边线比右边线高，则*(2,6)、(3,6)、(4,6)、(5,6)* 这4个解划去不用计算（纵向划去））。
```
  1 2 3 4 5 6
1 x ------- o
2 x x
3 x x x
4 x x x x
5 x x x x x
6 x x x x x x
```
第二次计算*(2,6)* ，如果左大于右，则应该删除解空间中*(3,6)、(4,6)、(5,6)* ，此处去掉了n-3个解。**相当于右边指针左移一位，以5作为右边终止点**。
```
  1 2 3 4 5 6
1 x ------- o
2 x x       o
3 x x x     |
4 x x x x   |
5 x x x x x |
6 x x x x x x
```
以此类推下去，最终我们总共计算了`n-1`种case，实现了线性时间复杂度。
```
  1 2 3 4 5 6
1 x ------- o
2 x x - o o o
3 x x x o | |
4 x x x x | |
5 x x x x x |
6 x x x x x x
```

# Solution
```
class Solution {
public:
    int maxArea(vector<int>& height) {
        int max=0;
        int i=0,j=height.size()-1;
        while(i<j)
        {
            int cur_area=(j-i)*min(height[i],height[j]);
            if(cur_area>max)
                max=cur_area;
            if(height[i]<height[j])
                i++;
            else
                j--;
        }
        return max;
    }
};
```
