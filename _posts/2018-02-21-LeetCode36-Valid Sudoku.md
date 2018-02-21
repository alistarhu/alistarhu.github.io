---
layout:     post
title:      LeetCode 36. Valid Sudoku
subtitle:   
date:       2018-02-21
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 36. Valid Sudoku - Medium

# Description
Determine if a Sudoku is valid, according to: Sudoku Puzzles - The Rules.

The Sudoku board could be partially filled, where empty cells are filled with the character `'.'`.

![sudoku_example](https://raw.githubusercontent.com/AlistarHu/alistarhu.github.io/master/img/Leetcode36_sudoku_example.png)

**Note:** A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.

# Example
```

```

# Analysis
合法数独要求每行、每列、每个宫格中都包含数字1-9不能有重复。我们使用三个数组分别记录行、列、宫中每个数字出现次数，数组第一维表示有9个行列宫，数组第二维表示对应数字1-9。如果数组中有一个数字出现次数>1，则说明该数独不合法。

# Solution
```
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        string charmap[]={"0","1","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
        vector<string> res;
        if(digits.size()==0)
            return res;
        res.push_back("");
        for(int i=0;i<digits.size();i++)
        {
            string cur_str=charmap[digits[i]-'0'];
            vector<string> tmp_res;
            for(int j=0;j<res.size();j++)
            {
                for(int k=0;k<cur_str.size();k++)
                    tmp_res.push_back(res[j]+cur_str[k]);
            }
            res=tmp_res;
        }
        return res;
    }
};
```
