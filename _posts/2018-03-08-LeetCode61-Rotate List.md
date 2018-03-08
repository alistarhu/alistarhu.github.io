---
layout:     post
title:      LeetCode 61. Rotate List
subtitle:   
date:       2018-03-08
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 61. Rotate List - Medium

# Description
Given a list, rotate the list to the right by k places, where k is non-negative.

# Example
```
For example,
Given 1->2->3->4->5->NULL and k = 2,

return 4->5->1->2->3->NULL.
```

# Analysis
题目要求将链表中最后的k个元素翻转，这里首先将链表形成一个环，根据k的值寻找到新的头节点，然后在相应位置断开即可。

注意：这里k的值可能比链表长度还要长，这里进行了取模的操作`k=k%len`

# Solution
```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        if(head==NULL)
            return head;
        ListNode* pNode=head;
        ListNode* newHead;
        int len=1;
        while(pNode->next!=NULL)
        {
            len++;
            pNode=pNode->next;
        }
        pNode->next=head;   // circle the link
        k=k%len;
        if(k!=0)
        {
            // Find the new start
            for(int i=0;i<len-k;i++)    
                pNode=pNode->next;
            newHead=pNode->next;
            pNode->next=NULL;
        }
        else
        {
            pNode->next=NULL;
            newHead=head;    // k==len means no need change
        }
        return newHead;
    }
};
```
