# Longest Valid Parentheses

[Leetcode](https://leetcode.com/problems/longest-valid-parentheses/)


題意： 給定一個字串只包含括號，找出最長的合法括號


解題思路：

updated on 2015.12.21

使用dp來解，網友[Lexi]() 提供以下思路：

- d[i]: 以i開頭的最長valid parentheses有多長。

- d[i] =
    - if  (str[i] == ")")，以右括號開頭必定invalid，d[i] = 0
    
    - if (str[i] == "(")，以左括號開頭

        - 我們想看對應的有木有右括號。因為d[i + 1]代表的sequence肯定是左括號開頭右括號結尾，所以我們想catch((…))這種情況。j = i + 1 + d[i + 1]，正好就是str[i]後面越過完整sequence的下一個，若是右括號，d[i] = 2 + d[i + 1]
        
        - 除此之外，還有包起來後因為把後面的右括號用了而導致跟再往後也連起來了的情況，如((..))()()()。所以d[i]還要再加上j後面那一段的d[j + 1]


```java
public class Solution {
    public int longestValidParentheses(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        
        int max = 0;
        int len = s.length();
        int[] dp = new int[len];
        
        // dp[i] means substring starts with i has max valid length of dp[i]
        dp[len - 1] = 0;
        
        for (int i = s.length() - 2; i >= 0; i--) {
            if (s.charAt(i) == ')') {
                dp[i] = 0;
            } else {
                int j = (i + 1) + dp[i + 1];
                if (j < len && s.charAt(j) == ')') {
                    // (()()) 的外包情況
                    dp[i] = dp[i + 1] + 2;
                    if (j + 1 < s.length()) {
                        //()() 的後面還有的情況
                        dp[i] += dp[j + 1];
                    }
                    
                }
            }
            max = Math.max(max, dp[i]);
        }
        
        return max;
    }
}
```

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

---
###Reference
1. https://leetcodenotes.wordpress.com/2013/10/19/leetcode-longest-valid-parentheses/