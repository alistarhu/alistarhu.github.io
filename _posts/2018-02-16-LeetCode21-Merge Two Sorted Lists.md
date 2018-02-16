---
layout:     post
title:      LeetCode 21. Merge Two Sorted Lists
subtitle:   
date:       2018-02-16
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 21. Merge Two Sorted Lists - Easy

# Description
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

# Example
```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

# Analysis
- 题目要求将两个链表合并成一个链表，这里需要注意头节点的确定。
- 使用两个指针分别指向两个待合并的链表，将两个指针中较小元素连接到新链表上，同时指针后移一位，如此重复下去……直至两个链表都为空，表示链表合并完成。

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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* pHead=NULL;
        // Set the head node
        if(l1==NULL)
            return l2;
        else if(l2==NULL)
            return l1;
        else
        {
            if(l1->val<=l2->val)
            {
                pHead=l1;
                l1=l1->next;
            }
            else
            {
                pHead=l2;
                l2=l2->next;
            }
        }
        // Merge two list
        ListNode* pNode=pHead;
        while(l1!=NULL&&l2!=NULL)
        {
            if(l1->val<=l2->val)
            {
                pNode->next=l1;
                l1=l1->next;
            }
            else
            {
                pNode->next=l2;
                l2=l2->next;
            }
            pNode=pNode->next;    
        }
        if(l1==NULL)
            pNode->next=l2;
        else
            pNode->next=l1;
        return pHead;
    }
};
```
