---
layout:     post
title:      LeetCode 2. Add Two Numbers
subtitle:   
date:       2018-01-23
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 2. Add Two Numbers - Medium

# Description
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

# Example
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

# Analysis
- 依次读取两个链表的value值进行求和，使用一个变量存储进位值。

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int carry = 0;
        ListNode* listHead = new ListNode(0);
        ListNode* curlist = listHead;
        while(l1!=NULL||l2!=NULL||carry)
        {
            int sum=0;
            if(l1!=NULL)
            {
                sum+=l1->val;
                l1=l1->next;
            }
            if(l2!=NULL)
            {
                sum+=l2->val;
                l2=l2->next;
            }
            sum=sum+carry;
            carry=sum/10;
            ListNode* tmplist=new ListNode(sum%10);
            curlist->next=tmplist;
            curlist=curlist->next;
        }
        return listHead->next;
    }
};
```
