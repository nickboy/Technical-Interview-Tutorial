#Interleaving String

[原題網址](http://www.lintcode.com/en/problem/interleaving-string/)

解題思路：f[i][j]：第一個字串取前i個字元，第二個字串取前j個字元，能否組成新字串的前i+j個字元

>[注意] 除了判斷當前字元是否相同外，別忘了確保之前的條件皆成立，即判斷 f[i-1][j] 與 f[i][j-1]

```java
public boolean isInterleave(String s1, String s2, String s3) {
    // res[i][j] 表示s1的前i個字符和s2前j個字符是否能交替組今s3的前i+j個字符
    int lenS1 = s1.length();
    int lenS2 = s2.length();
    int lenS3 = s3.length();
    boolean[][] res = new boolean[lenS1+1][lenS2+1];
    
    if (lenS1 + lenS2 != lenS3) {
        return false;
    }
    //s3為空，則s1與s2都不需取，必為true
    res[0][0] = true;
    //只取s1來湊s3
    for (int i = 1; i <= lenS1; i++) {
        res[i][0] = (s1.charAt(i-1) == s3.charAt(i-1));
    }
    //只取s2來湊s3
    for (int i = 1; i <= lenS2; i++) {
        res[0][i] = (s2.charAt(i-1) == s3.charAt(i-1));
    }
    
    for (int i = 1; i <= lenS1; i++) {
        for (int j = 1; j <= lenS2; j++) {
            //只要確認兩個方案任一為true即為true
            //第一個代表取s1的第i個字符給s3用
            //第二個代表取s2的第j個字符給s3用
            res[i][j] = res[i-1][j] && (s1.charAt(i-1) == s3.charAt(i+j-1)) ||
                        res[i][j-1] && (s2.charAt(j-1) == s3.charAt(i+j-1));
        }
    }
    
    return res[lenS1][lenS2];
    
}
```

>Time Complexity O($$N^{2}$$)