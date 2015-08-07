# Sort List
[原題網址](http://www.lintcode.com/en/problem/sort-list/)


```java
public ListNode sortList(ListNode head) {  
        
        if ( head == null || head.next == null ) {
            return head;
        }
        
        ListNode mid = findMiddle(head);
        ListNode right = sortList(mid.next);
        mid.next = null;
        ListNode left = sortList(head);
        
        return mergeLists(left, right);
    }
    
    public ListNode findMiddle(ListNode head) {
        ListNode slow = head, fast = head.next;
        while ( fast != null && fast.next != null ) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
    
    public ListNode mergeLists(ListNode head1, ListNode head2) {
        ListNode dummy = new ListNode(0);
        ListNode head = dummy;
        while ( head1 != null && head2 != null ) {
            if ( head1.val < head2.val ) {
                head.next = head1;
                head1 = head1.next;
            } else {
                head.next = head2;
                head2 = head2.next;
            }
            head = head.next;
        }
        if ( head1 != null ) {
            head.next = head1;
        }
        if ( head2 != null ) {
            head.next = head2;
        }
        return dummy.next;
    }
```