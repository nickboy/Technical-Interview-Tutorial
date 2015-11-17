# Find the Celebrity

[Leetcode](https://leetcode.com/problems/find-the-celebrity/)

題意：


解題思路：

從陣列的兩頭夾擊，假設有兩人 l 與 r，有以下兩個情況
1. 如果 l 認識 r，則 l 就不是名人，則 l++
2. 如果 r 認識 l，則 r 就不是名人，則 r--


最後還需要再檢查一遍是否所有人都認識 l 且 l 不認識任何人，其程式碼如下：

```java
/* The knows API is defined in the parent class Relation.
      boolean knows(int a, int b); */

public class Solution extends Relation {
    public int findCelebrity(int n) {
        if (n == 0) {
            return 0;
        }
        
        int l = 0;
        int r = n - 1;
        
        while (l < r) {
            if (knows(l, r)) {
                l++;
            } else {
                r--;
            }
        }
        
        for (int i = 0; i < n; i++) {
            if (i != l) {
                if (knows(l, i) || !knows(i, l)) {
                    return -1;
                }
            }
        }
        
        return l;
    }
}
```