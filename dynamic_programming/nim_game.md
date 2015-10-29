# Nim Game

[Leetcode]()

題意：


解題思路：

類似coins in linee那題博奕式遞迴。


一開始使用遞迴作會超時，

```java
public class Solution {
    public boolean canWinNim(int n) {
        if (n <= 3) {
            return true;
        }
        boolean caseOne = canWinNim(n-2);
        boolean caseTwo = canWinNim(n-3);
        boolean caseThree = canWinNim(n-4);
        boolean caseFour = canWinNim(n-5);
        boolean caseFive = canWinNim(n-6);
        
        return (caseOne && caseTwo && caseThree) || 
               (caseTwo && caseThree && caseFour) || 
               (caseThree && caseFour && caseFive);
    }
}
```