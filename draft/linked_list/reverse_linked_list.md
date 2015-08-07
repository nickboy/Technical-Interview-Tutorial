# Reverse Linked List
[原題網址](http://www.lintcode.com/en/problem/reverse-linked-list/)

>Reverse a linked list.


```java
public ListNode reverse(ListNode head) {
    ListNode current = null;
    
    while ( head != null ) {
        ListNode temp = head.next;
        head.next = current;
        current = head;
        head = temp;
    }
    return current;
}
```