---
layout:     post
title:      LeetCode 24. Swap Nodes in Pairs
subtitle:   
date:       2018-02-18
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 24. Swap Nodes in Pairs - Medium

# Description
Given a linked list, swap every two adjacent nodes and return its head.

# Example
```
For example,
Given `1->2->3->4`, you should return the list as `2->1->4->3`.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.
```

# Analysis
题目要求将链表中节点两两交换，主要涉及链表指针操作，pNode指向待交换的两个节点的前一个节点

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
    ListNode* swapPairs(ListNode* head) {
        if(head==NULL||head->next==NULL)
            return head;
        // Deal with head node
        ListNode* newhead=head->next;
        head->next=head->next->next;
        newhead->next=head;
        // Swap each two node after 2
        ListNode* pNode=newhead->next;
        while(pNode->next!=NULL&&pNode->next->next!=NULL)
        {
            ListNode* tmp=pNode->next;
            pNode->next=pNode->next->next;
            tmp->next=tmp->next->next;
            pNode->next->next=tmp;
            pNode=pNode->next->next;
        }
        return newhead;
    }
};
```
