# Excel Sheet Column TItle

[Leetcode](https://leetcode.com/problems/excel-sheet-column-title/)

題意：

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:
```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
```

解題思路：

```java
public class Solution {
    public String convertToTitle(int n) {
        StringBuilder sb = new StringBuilder();
        while (n != 0) {
            int remainder = n % 26;
            n = n / 26;
            if (remainder == 0) {
                sb.append('Z');
                n--;
            } else {
                char c = (char)(remainder - 1 + 'A');
                sb.append(c);
            }
        }
        
        return sb.reverse().toString();
    }
}
```