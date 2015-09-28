#Add Binary

[]()

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