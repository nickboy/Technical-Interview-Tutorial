# Longest Valid Parentheses

[Leetcode](https://leetcode.com/problems/longest-valid-parentheses/)


題意： 給定一個字串只包含括號，找出最長的合法括號


解題思路：

暴力解，把任何組合全丟進去isvalid的方法來判斷，時間複雜度約O(N^3)

程式碼如下，在leetcode會超時：

```java
public class Solution {
    public int longestValidParentheses(String s) {
        int maxLength = 0;
        if (s == null || s.length() == 0){
            return maxLength;
        }
        int j = 0;
        for (int i = 0; i < s.length() && j <= s.length(); i++) {
            String substring = s.substring(i, j);
            while(isValid(substring)) {
                maxLength = Math.max(maxLength, j - i + 1);
                j++;
                substring = s.substring(i, j);
            }
        }
        
        return maxLength;
    }
    
    private boolean isValid(String s) {
        
        if (s == null || s.length() == 0) {
            return true;
        }
        
        char[] charArray = s.toCharArray();
        Stack<Character> stack = new Stack<Character>();
        for (int i = 0; i < charArray.length; i++) {
            if (charArray[i] == ')') {
                if (stack.isEmpty() || stack.peek() != ')') {
                    return false;
                }
                stack.pop();
            } else {
                stack.push(charArray[i]);
            }
        }
        return stack.isEmpty();
    }
}
```

另外可用 stack 法，stack中存放尚未配對的括號，只要一但找到能配對的括號，則pop掉，並算長度，否則就push進去。

程式碼如下：

```java
public class Solution {
    public int longestValidParentheses(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        
        Stack<Integer> stack = new Stack<Integer>();
        int res = 0;
        for (int i = 0; i < s.length(); i++) {
            if (!stack.isEmpty() && s.charAt(i) == ')' && s.charAt(stack.peek()) == '(') {
                stack.pop();
                if (stack.isEmpty()) {
                    res = i + 1;
                } else {
                    res = Math.max(res, i - stack.peek());
                }
            } else {
                stack.push(i);
            }
        }
        
        return res;
    }
}
```