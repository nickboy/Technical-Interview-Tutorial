# Palindrome Permutation II

[Leetcode](https://leetcode.com/problems/palindrome-permutation-ii/)


題意：

Given a string s, return all the palindromic permutations (without duplicates) of it. Return an empty list if no palindromic permutation could be form.

For example:

Given s = "aabb", return ["abba", "baab"].

Given s = "abc", return [].

解題思路：

使用dfs去作，再搭配ispalindrome來判斷是否為迴文，但複雜度太高，會超時，程式碼如下：

```java
public class Solution {
    List<String> res;
    boolean[] isVisited;
    public List<String> generatePalindromes(String s) {
        res = new ArrayList<String>();
        isVisited = new boolean[s.length()];
        if (s == null || s.length() == 0) {
            return res;
        }
        
        helper(s, new StringBuilder());
        return res;
        
    }
    
    private void helper(String s, StringBuilder sb) {
        if (sb.length() == s.length()) {
            if (isPalindrome(sb.toString())) {
                res.add(sb.toString());
            }
        }
        
        for (int i = 0; i < s.length(); i++) {
            if (isVisited[i]) {
                continue;
            }
            isVisited[i] = true;
            sb.append(s.charAt(i));
            helper(s, sb);
            sb.setLength(sb.length() - 1);
            isVisited[i] = false;
        }
    }
    
    private boolean isPalindrome(String s) {
        int start = 0;
        int end = s.length() - 1;
        while (start <= end) {
            if (s.charAt(start) != s.charAt(end)) {
                return false;
            }
            start++;
            end--;
        }
        
        return true;
    }
}
```