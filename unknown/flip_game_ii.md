# Flip Game II

[Leetcode](https://leetcode.com/problems/flip-game-ii/)

題意：

為 [Flip Game]() 的follow up，在此給定一個字串，來判斷是否先手會贏。

You are playing the following Flip Game with your friend: Given a string that contains only these two characters: + and -, you and your friend take turns to flip two consecutive "++" into "--". The game ends when a person can no longer make a move and therefore the other person will be the winner.

Write a function to determine if the starting player can guarantee a win.

For example, given s = "++++", return true. The starting player can guarantee a win by flipping the middle "++" to become "+--+".

Follow up:
Derive your algorithm's runtime complexity.

解題思路：

網友 [hanay](http://www.meetqun.com/thread-11570-1-1.html) 提供了清楚的回溯解法，使用dfs來幫助我們解這道題，程式碼如下：

"對每次回溯都檢查是否有走下一步的可能，如果沒有可能有下一步，意味著肯定是輸的，所以返回false。如果有下一步，檢查對手在下一步的基礎上是否保證會贏，如果對手在下一步基礎上保證會贏，則繼續尋找其他走法；如果對手在下一步不能保證會贏，意味著如果我們走該次走法，可以在以後的比賽中通過某種走法保證對手輸，返回true。如果發現無論怎麼走對手都會贏，也返回false。  

這樣的代碼複雜度是O（n！），如果輸入是一個長度為N的"+++++...+++"，T(N)=T(N-2)+T(N-3)+(T(2)+T(N-4))+(T(3)+T(N-5))+....+(T(N-5)+T(3))+(T(N-4)+T(2))+T(N-3)+T(N-2) = 2(T(2)+T(3) +..T(N-2))<N*T(N-2) = N(N-2)(N-4)..3*2 < n!"

```java
public class Solution {
    public boolean canWin(String s) {
        
        if (s == null || s.length() < 2) {
            return false;
        }
        
        return dfs(s);
    }
    
    public boolean dfs(String s) {
        StringBuilder sb = new StringBuilder();
        sb.append(s);
        for (int i = 0; i < sb.length() - 1; i++) {
            if (s.charAt(i) == '+' && s.charAt(i + 1) == '+') {
                sb.setCharAt(i, '-');
                sb.setCharAt(i + 1, '-');
                
                // 接下來再跑dfs此時是換成對手，如果對手一定輸，代表先手一定贏
                if (!dfs(sb.toString())) {
                    return true;
                }
                // 記得改回來
                sb.setCharAt(i, '+');
                sb.setCharAt(i + 1, '+');
            }
        }
        
        // 沒有半個方式可以贏的話，那先手必輸
        return false;
    }
}
```

網友[stellari](https://leetcode.com/discuss/64344/theory-matters-from-backtracking-128ms-to-dp-0ms) 提供了超詳細解說，還有game theory的解法，目前沒時間好好看，先留著之後再回來看。

---
###Reference
1. http://www.meetqun.com/thread-11570-1-1.html
2. https://leetcode.com/discuss/64344/theory-matters-from-backtracking-128ms-to-dp-0ms