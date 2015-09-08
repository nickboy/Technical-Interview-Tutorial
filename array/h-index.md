#H-Index

[原題網址](https://leetcode.com/problems/h-index/)

題意：
A scientist has index h if h of his/her N papers have at least h citations each, and the other N − h papers have no more than h citations each.

解題思路：

```java
public int hIndex(int[] citations) {
    
    if (citations == null || citations.length == 0) {
        return 0;
    }
    
    int len = citations.length;
    Arrays.sort(citations);
    for (int i = 0; i < len; i++) {
        if (citations[i] >= len - i) {
            return len - i;
        }
    }
    return 0;
}
```