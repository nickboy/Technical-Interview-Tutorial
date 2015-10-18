# Word Ladder

[原題網址](http://www.lintcode.com/en/problem/word-ladder/)

> Given two words (start and end), and a dictionary, find the length of shortest transformation sequence from start to end, such that:

> 1. Only one letter can be changed at a time
> 2. Each intermediate word must exist in the dictionary


解題思路：

使用bfs來幫助我們解這道題，每一次只更換一個字元，並檢查是否在dict中，若在的話，便加入queue以利下一次繼續往下搜尋，每次加入queue中時，記得把dict相同的字刪除，以避免循環的問題發生。


```java
public int ladderLength(String start, String end, Set<String> dict) {
    // write your code here
    
    Queue<String> queue = new LinkedList<String>();
    queue.offer(start);
    dict.remove(start);
    int level = 1;
    
    while ( !queue.isEmpty() ) {
        int size = queue.size();
        for ( int i = 0 ; i < size ; i++ ) {
            String current = queue.poll();
            for ( char c = 'a' ; c <= 'z' ; c++ ) {
                for ( int j = 0 ; j < current.length() ; j++ ) {
                    if ( current.charAt(j) == c ) {
                        continue;
                    }
                    String temp = replace(current, j, c);
                    if ( temp.equals(end) ) {
                        return level+1;
                    }
                    if ( dict.contains(temp) ) {
                        queue.offer(temp);
                        dict.remove(temp);
                    } 
                }
            }
        }
        level++;
    }
    return 0;
}

public String replace(String origin, int pos, char c) {
    char[] chars = origin.toCharArray();
    chars[pos] = c;
    return new String(chars);
}
```



---
#Reference
1. http://www.cnblogs.com/TenosDoIt/p/3443512.html