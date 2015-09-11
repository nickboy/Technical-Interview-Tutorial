#Remove Duplicates from Sorted List II

[]()

題意：為 [Remove Duplicates from Sorted List ](linked_list/remove_duplicates_from_sorted_list.md) 的變形，只要遇到有相同的值，則把所有節點全刪了。

解題思路：

由於 head 可能也有重覆，因此 head 有可能會改變，在此我們需要使用 dummy node 來輔助，先將相同的值紀錄下來，不斷的拿 ```head.next``` 與 該值作比較，

* 若相同，則改變head.next的值
* 若不同，則移動head

其程式碼如下：

>雖然程式碼不難，但在操作時常常會忽略細節或搞混，必熟練！

```java
public static ListNode deleteDuplicates(ListNode head) {
    
    if (head == null) {
        return head;
    }
    
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    head = dummy;
    
    while (head.next != null && head.next.next != null) {
        if (head.next.val == head.next.next.val) {
            int val = head.next.val;
            while (head.next != null && head.next.val == val) {
                head.next = head.next.next;
            }
        } else {
            head = head.next;
        }
    }
    
    return dummy.next;
}
```