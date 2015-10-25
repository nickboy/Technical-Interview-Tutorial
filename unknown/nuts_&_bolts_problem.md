# Nuts & Bolts Problem

[Lintcode](http://www.lintcode.com/en/problem/nuts-bolts-problem/)

題意：



解題思路：

還不是很理解這題想作什麼，主要是要排序nuts與bolts，但nut不能跟nut比，只能跟map 過去的bolts來比。

引用網友 [mnmunknown](http://www.1point3acres.com/bbs/forum.php?mod=viewthread&action=printable&tid=138798) 的思路如下

"基本思路很簡單，由於 compare 規定只能按（nut, bolt）的順序放， 先從 nut 裡選一個做 pivot ，按此 pivot 與 bolts array 進行比較並且進行 partition ; 而後返回 pivot element 的 index ，代表對應原先選擇的 nut 的 bolt ，並且以此元素回到 nuts array 裡面進行 partition ； 最後遞歸處理左右兩邊。"

待之後再理解

九章的解法如下：

```java

/**
 * public class NBCompare {
 *     public int cmp(String a, String b);
 * }
 * You can use compare.cmp(a, b) to compare nuts "a" and bolts "b",
 * if "a" is bigger than "b", it will return 1, else if they are equal,
 * it will return 0, else if "a" is smaller than "b", it will return -1.
 * When "a" is not a nut or "b" is not a bolt, it will return 2, which is not valid.
*/
public class Solution {
    /**
     * @param nuts: an array of integers
     * @param bolts: an array of integers
     * @param compare: a instance of Comparator
     * @return: nothing
     */
    public void sortNutsAndBolts(String[] nuts, String[] bolts, NBComparator compare) {
        if (nuts == null || nuts.length == 0 || bolts == null || bolts.length == 0) {
            return;
        }
        qsort(nuts, bolts, compare, 0, nuts.length - 1);
    }
    
    private void qsort(String[] nuts, String[] bolts, NBComparator compare, int lower, int upper) {
        if (lower >= upper) {
            return;
        }
        
        int pivot = partition(nuts, bolts[lower], compare, lower, upper);
        
        partition(bolts, nuts[pivot], compare, lower, upper);
        
        qsort(nuts, bolts, compare, lower, pivot);
        qsort(nuts, bolts, compare, pivot + 1, upper);
        
    }
    
    private int partition(String[] str, String pivot, NBComparator compare, int lower, int upper) {
        int m = lower;
        for (int i = lower + 1; i <= upper; i++) {
            if (compare.cmp(str[i], pivot) == -1 ||
                compare.cmp(pivot, str[i]) == 1) {
                    m++;
                    swap(str, i, m);
            } else if (compare.cmp(str[i], pivot) == 0 ||
                        compare.cmp(pivot, str[i]) == 0) {
                swap(str, i, lower);
                i--;
            }
        }
        
        swap(str, m, lower);
        return m;
    }
    
    private void swap(String[] str, int l, int r) {
        String temp = str[l];
        str[l] = str[r];
        str[r] = temp;
    }
};
```

---
###Reference
1. http://www.jiuzhang.com/solutions/nuts-bolts-problem/
2. http://www.1point3acres.com/bbs/forum.php?mod=viewthread&action=printable&tid=138798