#Compare Strings

解題思路：利用

```java
public boolean compareStrings(String A, String B) {
    HashMap<Character, Integer> map = new HashMap<Character,Integer>();
    for (int i = 0; i < A.length(); i++) {
        char c = A.charAt(i);
        if (!map.containsKey(c)) {
            map.put(c, 1);
        } else {
            map.put(c, map.get(c) + 1);
        }
    }
    for (int i = 0; i < B.length(); i++) {
        char c = B.charAt(i);
        if (!map.containsKey(c) || map.get(c) == 0) {
            return false;
        } else {
            map.put(c, map.get(c) - 1);
        }
    }
    return true;
}
```