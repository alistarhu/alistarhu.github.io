---
layout:     post
title:      LeetCode 71. Simplify Path
subtitle:   
date:       2018-03-12
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 71. Simplify Path - Medium

# Description
Given an absolute path for a file (Unix-style), simplify it.

# Example
```
path = "/home/", => "/home"
path = "/a/./b/../../c/", => "/c"
```

# Analysis
这道题要求将一个Unix的路径进行简化后输出。这里主要考察字符串的操作，**特别注意对于一些特殊输入的处理**

# Solution
```
class Solution {
public:
    string simplifyPath(string path) {
        int start=0;
        vector<string> dir;
        if(path[path.size()-1]!='/')
            path.push_back('/');
        for(int i=1;i<path.size();i++)
        {
            if(path[i]=='/'&&path[i]==path[i-1])
                start=i;
            else if(path[i]=='/')
            {
                string tmp=path.substr(start+1,i-start-1);
                start=i;
                if(tmp=="..")
                {
                    if(!dir.empty())
                        dir.pop_back();
                }
                else if(tmp==".")
                    continue;
                else
                    dir.push_back(tmp);

            }
        }
        string res="/";
        for(int i=0;i<dir.size();i++)
        {
            if(i!=dir.size()-1)
                res+=dir[i]+'/';
            else
                res+=dir[i];
        }
        return res;
    }
};
```
