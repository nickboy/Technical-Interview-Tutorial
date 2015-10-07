#Add Binary

[Lintcode](http://www.lintcode.com/en/problem/add-binary/)

題意：

Given two binary strings, return their sum (also a binary string).

Example

```a = 11```

```b = 1```

Return ```100```

解題思路：

從兩個字串的最右邊開始 (即字串的lenght - 1)，一一往左推進，直到其中一方到底了，接著再把還沒到底的字串一一與carry相加再繼續往左推進，直到該字串也到底了，最後看carry是否為1，若是則再把carry附到最前。

程式碼如下，有點長，日後有改良版再附上：

```java
public String addBinary(String a, String b) {
    if (a == null && b == null) {
        return "";
    }
    if (a.length() == 0 || b.length() == 0) {
        return (a.length() == 0) ? a : b;
    }
    
    StringBuilder sb = new StringBuilder();
    int lenA = a.length();
    int lenB = b.length();
    
    int posA = lenA - 1;
    int posB = lenB - 1;
    int carry = 0;
    while (posA >= 0 && posB >= 0) {
        int digitA = a.charAt(posA) - '0';
        int digitB = b.charAt(posB) - '0';
        int sum = carry + digitA + digitB;
        carry = sum / 2;
        sum = sum % 2;
        sb.insert(0, Integer.toString(sum));
        posA--;
        posB--;
    }
    
    if (posA >= 0) {
        while ( posA >= 0) {
            int digitA = a.charAt(posA) - '0';
            int sum = carry + digitA;
            carry = sum / 2;
            sum = sum % 2;
            sb.insert(0, Integer.toString(sum));
            posA--;
        }
    } else if (posB >= 0) {
        while (posB >= 0) {
            int digitB = b.charAt(posB) - '0';
            int sum = carry + digitB;
            carry = sum / 2;
            sum = sum % 2;
            sb.insert(0, Integer.toString(sum));
            posB--;
        }
    }
    if (carry == 1){
        sb.insert(0, Integer.toString(carry));
    }
    
    return sb.toString();
    
    
}
```

以下為 [九章解法](http://www.jiuzhang.com/solutions/add-binary/)：

先把較長字串換到前面，可以減化後面的程式碼

```java
public String addBinary(String a, String b) {
    if(a.length() < b.length()){
        String tmp = a;
        a = b;
        b = tmp;
    }
    
    int pa = a.length()-1;
    int pb = b.length()-1;
    int carries = 0;
    String rst = "";
    
    while(pb >= 0){
        int sum = (int)(a.charAt(pa) - '0') + (int)(b.charAt(pb) - '0') + carries;
        rst = String.valueOf(sum % 2) + rst;
        carries = sum / 2;
        pa --;
        pb --;
    }
    
    while(pa >= 0){
        int sum = (int)(a.charAt(pa) - '0') + carries;
        rst = String.valueOf(sum % 2) + rst;
        carries = sum / 2;
        pa --;
    }       
    
    if (carries == 1)
        rst = "1" + rst;
    return rst;
}
```

updated 2015.10.6

```java
public class Solution {
    public String addBinary(String a, String b) {
        
        
        if (a == null || a.length() == 0) {
            return b;
        } else if (b == null || b.length() == 0) {
            return a;
        } 
        
        StringBuilder sb = new StringBuilder();
        int idxA = a.length() - 1;
        int idxB = b.length() - 1;
        int carry = 0;
        while (idxA >= 0 && idxB >= 0) {
            int aBit = a.charAt(idxA) - '0';
            int bBit = b.charAt(idxB) - '0';
            int sum = aBit + bBit + carry;
            sb.append(sum % 2);
            carry = sum / 2;
            idxA--;
            idxB--;
        }
        while (idxA >= 0) {
            int sum = carry + (a.charAt(idxA) - '0');
            sb.append(sum % 2);
            carry = sum / 2;
            idxA--;
        }
        while (idxB >= 0) {
            int sum = carry + (b.charAt(idxB) - '0');
            sb.append(sum % 2);
            carry = sum / 2;
            idxB--;
        }
        if (carry == 1) {
            sb.append('1');
        }
        
        return sb.reverse().toString();
    }
}
```
---
###Reference
1. http://www.jiuzhang.com/solutions/add-binary/