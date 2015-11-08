# Zigzag Iterator

[]()

題意：

Given two 1d vectors, implement an iterator to return their elements alternately.

For example, given two 1d vectors:
```
v1 = [1, 2]
v2 = [3, 4, 5, 6]
```
By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1, 3, 2, 4, 5, 6].

Follow up: What if you are given k 1d vectors? How well can your code be extended to such cases?

Clarification for the follow up question - Update (2015-09-18):
The "Zigzag" order is not clearly defined and is ambiguous for k > 2 cases. If "Zigzag" does not look right to you, replace "Zigzag" with "Cyclic". For example, given the following input:
```
[1,2,3]
[4,5,6,7]
[8,9]
```
It should return [1,4,8,2,5,9,3,6,7].

解題思路：

用一個queue交錯的放，其程式碼如下：

```java
public class ZigzagIterator {
    
    Queue<Integer> q = new LinkedList<Integer>();
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        int idx1 = 0;
        int idx2 = 0;
        int idx = 0;
        while(idx1 < v1.size() && idx2 < v2.size()) {
            if (idx % 2 == 0) {
                q.offer(v1.get(idx1));
                idx1++;
            } else {
                q.offer(v2.get(idx2));
                idx2++;
            }
            idx++;
        }
        
        if (idx1 < v1.size()) {
            while (idx1 < v1.size()) {
                q.offer(v1.get(idx1));
                idx1++;
            }
        } else if (idx2 < v2.size()) {
            while (idx2 < v2.size()) {
                q.offer(v2.get(idx2));
                idx2++;
            }
        }
    }

    public int next() {
        if (!q.isEmpty()) {
            return q.poll();
        }
        return -1;
    }

    public boolean hasNext() {
        return !q.isEmpty();
    }
}

/**
 * Your ZigzagIterator object will be instantiated and called as such:
 * ZigzagIterator i = new ZigzagIterator(v1, v2);
 * while (i.hasNext()) v[f()] = i.next();
 */
```
