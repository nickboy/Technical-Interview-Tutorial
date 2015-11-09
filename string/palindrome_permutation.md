# Palindrome Permutation

[]()

題意：

給定一個字串，判所是否可以排成迴文


解題思路：

使用一個hash map分別紀錄每個character的個數，接著根據以下情況來判斷

1. 如果字串長度為偶數，則所有字元的字數皆為偶數
2. 如果字串長度為奇數，則只能有一個字元的字數為奇數，其他皆為偶數


程式碼如下：

```java
public class Solution {
    public boolean canPermutePalindrome(String s) {
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        for (int i = 0; i < s.length(); i++) {
            char cur = s.charAt(i);
            if (!map.containsKey(cur)) {
                map.put(cur, 0);
            }
            map.put(cur, map.get(cur) + 1);
        }
        
        if (s.length() % 2 == 0) {
            for (int value : map.values()) {
                if (value % 2 == 1) {
                    return false;
                }
            }
            return true;
        } else {
            boolean one = false;
            for (int value : map.values()) {
                if (value % 2 == 1) {
                    if (!one) {
                        one = true;
                    } else {
                        return false;
                    }
                }
            }
            return true;
        }
    }
}
``