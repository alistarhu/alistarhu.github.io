---
layout:     post
title:      LeetCode 79. Word Search
subtitle:   
date:       2018-03-15
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 79. Word Search - Medium

# Description
Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

# Example
```
For example,
Given board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
word = "ABCCED", -> returns true,
word = "SEE", -> returns true,
word = "ABCB", -> returns false.
```

# Analysis
题意是，给定一个字符串，能否从一个二维字符数组中找出一条路径，使得路径形成的字符串与给定字符串相同。

这道题采用回溯法（深度优先搜索DFS）思想。每一步从当前位置向其四周（上、下、左、右）进行搜索，逐层向下递归查找。如果查找的层数与所求字符串长度相同，表明找到了结果，返回true。

# Solution
```
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        bool res=false;
        vector<vector<int>> used(board.size(),vector<int>(board[0].size(),0));
        for(int i=0;i<board.size();i++)
            for(int j=0;j<board[0].size();j++)
                if(dfs(board,word,i,j,0,used))
                    return true;
        return false;
    }

    bool dfs(vector<vector<char>>& board,string& word,int x,int y,int idx,vector<vector<int>>& used)
    {
        bool res=false;
        if(word[idx]==board[x][y])
        {
            if(idx==word.size()-1)  // Find a solution
                return true;
            else    // Find the next word
            {
                used[x][y]=1;
                // Only one pass is the right solution
                if(x>0&&used[x-1][y]==0&&dfs(board,word,x-1,y,idx+1,used))
                    res=true;
                else if(x+1<board.size()&&used[x+1][y]==0&&dfs(board,word,x+1,y,idx+1,used))
                    res=true;
                else if(y>0&&used[x][y-1]==0&&dfs(board,word,x,y-1,idx+1,used))
                    res=true;
                else if(y+1<board[0].size()&&used[x][y+1]==0&&dfs(board,word,x,y+1,idx+1,used))
                    res=true;
                used[x][y]=0;
            }
        }
        return res;  
    }
};
```
