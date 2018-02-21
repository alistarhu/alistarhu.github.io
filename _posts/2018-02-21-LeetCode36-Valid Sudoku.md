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
合法数独要求每行、每列、每个宫格中都包含数字1-9并且不能有重复。我们使用三个数组分别记录行、列、宫中每个数字出现次数，数组第一维表示有9个行列宫，数组第二维表示对应数字1-9。如果数组中有一个数字出现次数>1，则说明该数独不合法。

# Solution
```
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        int rowflag[9][9]={0};
        int colflag[9][9]={0};
        int gonflag[9][9]={0};
        for(int i=0;i<board.size();i++)
        {
            for(int j=0;j<board[0].size();j++)
            {
                if(board[i][j]!='.')
                {
                    int curNum=board[i][j]-'0'-1;
                    int gonidx=i/3*3+j/3;
                    // If curNum appear before is not valid
                    if(rowflag[i][curNum]!=0||colflag[j][curNum]!=0||gonflag[gonidx][curNum]!=0)
                        return false;
                    else
                    {
                        rowflag[i][curNum]=1;
                        colflag[j][curNum]=1;
                        gonflag[gonidx][curNum]=1;
                    }
                }
            }
        }
        return true;
    }
};
```
