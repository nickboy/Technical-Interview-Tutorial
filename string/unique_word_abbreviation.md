# Unique Word Abbreviation

[Leetcode](https://leetcode.com/problems/unique-word-abbreviation/)

題意：

An abbreviation of a word follows the form <first letter><number><last letter>. Below are some examples of word abbreviations:

a) it                      --> it    (no abbreviation)

     1
b) d|o|g                   --> d1g

              1    1  1
     1---5----0----5--8
c) i|nternationalizatio|n  --> i18n

              1
     1---5----0
d) l|ocalizatio|n          --> l10n
Assume you have a dictionary and given a word, find whether its abbreviation is unique in the dictionary. A word's abbreviation is unique if no other word from the dictionary has the same abbreviation.

Example: 
Given dictionary = [ "deer", "door", "cake", "card" ]

isUnique("dear") -> false

isUnique("cart") -> true

isUnique("cane") -> false

isUnique("make") -> true

解題思路：

```java
public class ValidWordAbbr {
    
    HashMap<String, HashSet<String>> map = new HashMap<String, HashSet<String>>();
    HashSet<String> set = new HashSet<String>();
    public ValidWordAbbr(String[] dictionary) {
        
        for (int i = 0; i < dictionary.length; i++) {
            String cur = dictionary[i];
            set.add(cur);
            if (cur.length() < 3) {
                if (!map.containsKey(cur)) {
                    map.put(cur, new HashSet<String>());
                    
                }
                map.get(cur).add(cur);
            } else {
                StringBuilder sb = new StringBuilder();
                sb.append(cur.charAt(0));
                sb.append(cur.length() - 2);
                sb.append(cur.charAt(cur.length() - 1));
                String key = sb.toString();
                if (!map.containsKey(key)) {
                    map.put(key, new HashSet<String>());
                }
                
                map.get(key).add(cur);
            }
        }
    }

    public boolean isUnique(String word) {
        if (word.length() < 3) {
            if (!map.containsKey(word)) {
                return true;
            }
            return map.get(word).size() == 1 && set.contains(word);
        } else {
            StringBuilder sb = new StringBuilder();
            sb.append(word.charAt(0));
            sb.append(word.length() - 2);
            sb.append(word.charAt(word.length() - 1));
            String key = sb.toString();
            if (!map.containsKey(key)) {
                return true;
            }
            return map.get(key).size() == 1 && set.contains(word);
        }
        
    }
}


// Your ValidWordAbbr object will be instantiated and called as such:
// ValidWordAbbr vwa = new ValidWordAbbr(dictionary);
// vwa.isUnique("Word");
// vwa.isUnique("anotherWord");
```