---
layout:     post
title:      LeetCode 19. Remove Nth Node From End of List
subtitle:   
date:       2018-02-16
author:     LeiHu
header-img: img/post-bg-leetcode.jpg
catalog: true
tags:
    - LeetCode
---
# 19. Remove Nth Node From End of List - Medium

# Description
Given a linked list, remove the nth node from the end of list and return its head.

**Note:** Given n will always be valid.Try to do this in one pass.

# Example
```
For example, Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```

# Analysis
这里需要删除倒数第n个节点，采用快慢指针的方法：快指针和慢指针之间的间隔保持为n，快慢指针同时向链表尾部移动；当快指针到达尾节点时，慢指针指向待删除节点的前一个节点，然后进行节点删除即可；这里对删除头节点的情况单独处理。

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* pFast=head;
        for(int i=0;i<n;i++)
            pFast=pFast->next;
        // If delete the first point
        if(pFast==NULL)
            return head->next;
        // pSlow at the position ahead of the delete point
        ListNode* pSlow=head;
        while(pFast->next!=NULL)
        {
            pFast=pFast->next;
            pSlow=pSlow->next;
        }
        pSlow->next=pSlow->next->next;
        return head;
    }
};
```
