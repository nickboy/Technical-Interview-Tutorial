# Remove Nth Node From End of List
Given a linked list, remove the nth node from the end of list and return its head.

```java
public class Solution {
    /**
     * @param head: The first node of linked list.
     * @param n: An integer.
     * @return: The head of linked list.
     */
    ListNode removeNthFromEnd(ListNode head, int n) {
        // write your code here
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode slow = dummy;
        
        while ( head != null && n > 0 ) {
            head = head.next;
            n--;
        }
        
        if ( n > 0 ) {
            return null;
        }
        
        while ( head != null ) {
            slow = slow.next;
            head = head.next;
        }
        
        slow.next = slow.next.next;
        
        return dummy.next;
    }
    
    // ListNode removeNthFromEnd(ListNode head, int n) {
    //     // write your code here
        
    //     ListNode dummy = new ListNode(0);
    //     dummy.next = head;
        
    //     ListNode target = dummy;
    //     for ( int i = 0 ; i < n ; i ++ ) {
    //         if ( head == null ) {
    //             return null;
    //         }
    //         head = head.next;
    //     }
        
    //     while ( head != null ) {
    //         target = target.next;
    //         head = head.next;
    //     }
    //     target.next = target.next.next;
        
    //     return dummy.next;
    // }
}
```