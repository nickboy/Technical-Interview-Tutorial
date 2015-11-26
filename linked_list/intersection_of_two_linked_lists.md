# Intersection of Two Linked Lists

[Leetcode](https://leetcode.com/problems/intersection-of-two-linked-lists/)

題意：

Write a program to find the node at which the intersection of two singly linked lists begins.


For example, the following two linked lists:
```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```
begin to intersect at node c1.


Notes:

If the two linked lists have no intersection at all, return null.
The linked lists must retain their original structure after the function returns.
You may assume there are no cycles anywhere in the entire linked structure.
Your code should preferably run in O(n) time and use only O(1) memory.



解題思路：


先找出兩條 list 的長度，接著長的那條先走lenA - lenB步，接著較短的那條也跟著一起走直到走到底或是找到交插口。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        
        if (headA == null || headB == null) {
            return null;
        }
        int lenA = 0;
        int lenB = 0;
        ListNode curA = headA;
        ListNode curB = headB;
        
        while (curA != null) {
            lenA++;
            curA = curA.next;
        }
        
        while (curB != null) {
            lenB++;
            curB = curB.next;
        }
        
        if (lenB > lenA) {
            ListNode temp = headA;
            headA = headB;
            headB = temp;
        }
        
        for (int i = 0; i < Math.abs(lenA - lenB); i++) {
            headA = headA.next;
        }
        
        while(headA != null && headB != null) {
            if (headA == headB) {
                return headA;
            }
            headA = headA.next;
            headB = headB.next;
        }
        
        return null;
    }
}
```

---
###Reference
1. http://www.cnblogs.com/yuzhangcmu/p/4128794.html