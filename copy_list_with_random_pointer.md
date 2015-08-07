# Copy List with Random Pointer



```java
public RandomListNode copyRandomList(RandomListNode head) {
    
    RandomListNode dummy = new RandomListNode(0);
    RandomListNode last = dummy, newNode;
    HashMap<RandomListNode, RandomListNode> map= new HashMap<RandomListNode, RandomListNode>();
    
    while ( head != null ) {
        if ( map.containsKey(head) ) {
            newNode = map.get(head);
        } else {
            newNode = new RandomListNode(head.label);
            map.put(head, newNode);
        }
        last.next = newNode;
        
        if ( head.random != null ) {
            if ( map.containsKey(head.random) ) {
                newNode = map.get(head.random);
            } else {
                newNode = new RandomListNode(head.random.label);
                map.put(head.random, newNode);
            }
            last.next.random = newNode;
        }
        last = last.next;
        head = head.next;
    }
    return dummy.next;   
}
```