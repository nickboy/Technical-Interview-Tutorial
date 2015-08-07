# Jump Game
[原題網址]
```java
public boolean canJump(int[] A) {
    // wirte your code here
    boolean[] can = new boolean[A.length];
    can[0] = true;

    for (int i = 1; i < A.length; i++) {
        for (int j = 0; j < i; j++) {
            if (can[j] && j + A[j] >= i) {
                can[i] = true;
                break;
            }
        }
    }
    return can[A.length - 1];
}
```

#Jump Game II

```java
public int jump(int[] A) {

    int[] result = new int[A.length];
    result[0] = 0;
    
    for (int i = 1; i < A.length; i++) {
        result[i] = Integer.MAX_VALUE;
        for (int j = 0; j < i; j++) {
            // j + A[j] >= i 為確定是否能由j跳到i，超過也沒關係
            // result[i] > result[j] + 1 為判斷目前的result是否為最小的，
            // 直接break可省時間，避免重覆計算
            if (j + A[j] >= i && result[i] > result[j] + 1) {
                result[i] = result[j] + 1;
                break;
            }
        }
    }
    return result[A.length - 1];
}
```