# Restore IP Addresses

[Leetcode](https://leetcode.com/problems/restore-ip-addresses/)

題意：

Given a string containing only digits, restore it by returning all possible valid IP address combinations.

For example:

Given "25525511135",

return ["255.255.11.135", "255.255.111.35"]. (Order does not matter)

解題思路：

引用網友 [愛做飯的小瑩子](http://www.cnblogs.com/springfor/p/3886409.html) 的思路

"利用循環遞歸解決子問題。對於每個段內數來說，最多3位最少1位，所以在每一層可以循環3次，來嘗試填段。因為IP地址最多4個分段，當層數是3的時候說明已經嘗試填過3個段了，那麼把剩餘沒填的數段接到結尾即可。

這個過程中要保證的是填的數是合法的，最後拼接的剩餘的數也是合法的。

 注意開頭如果是0的話要特殊處理，如果開頭是0，判斷整個串是不是0，不是的話該字符就是非法的。因為001，01都是不對的。"
 

其程式碼如下：

```java
public class Solution {
    List<String> res = new ArrayList<String>();
    public List<String> restoreIpAddresses(String s) {
        
        if (s == null || s.length() < 4 || s.length() > 12) {
            return res;
        }
        
        helper(s, 0, new String());
        return res;
    }
    
    //s表示剩下要處理的部份，temp表示已處理完的部份
    private void helper(String s, int start, String temp) {
        if (start == 3 && isValid(s)) {
            res.add(temp + s);
            return;
        }
        
        for (int i = 0; i < 3 && i < s.length() - 1; i++) {
            String str = s.substring(0, i + 1);
            if (isValid(str)) {
                helper(s.substring(i + 1, s.length()), start + 1, temp + str + ".");
            }
        }
    }
    
    private boolean isValid(String s) {
        //防止011這類的錯誤
        if (s.charAt(0) == '0') {
            return s.equals("0");
        }
        int val = Integer.parseInt(s);
        if (val < 0 || val > 255) {
            return false;
        } else {
            return true;
        }
    }
}
```

---
###Reference
1. http://www.cnblogs.com/springfor/p/3886409.html