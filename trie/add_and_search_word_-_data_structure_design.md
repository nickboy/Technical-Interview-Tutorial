# Add and Search Word - Data structure design

[Leetcode](https://leetcode.com/problems/add-and-search-word-data-structure-design/)


題意：

Design a data structure that supports the following two operations:
```
void addWord(word)
bool search(word)
```
search(word) can search a literal word or a regular expression string containing only letters a-z or .. A . means it can represent any one letter.

For example:
```
addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
```
Note:
You may assume that all words are consist of lowercase letters a-z.

解題思路：

主要使用 trie與dfs來作，其程式碼如下：

```java
public class WordDictionary {
    
    public class TrieNode {
        char c;
        HashMap<Character, TrieNode> children = new HashMap<Character, TrieNode>();
        boolean isLeaf = false;
        public TrieNode() {
            
        }
        
        public TrieNode(char c) {
            this.c = c;
        }
    }
    
    TrieNode root = new TrieNode();
    // Adds a word into the data structure.
    public void addWord(String word) {
        HashMap<Character, TrieNode> children = root.children;
        for (int i = 0; i < word.length(); i++) {
            char c = word.charAt(i);
            if (!children.containsKey(c)) {
                children.put(c, new TrieNode());
            }
            TrieNode t = children.get(c);
            children = t.children;
            
            if (i == word.length() - 1) {
                t.isLeaf = true;
            }
        }
    }

    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    public boolean search(String word) {
        return searchHelper(root, word);
    }
    
    public boolean searchHelper(TrieNode root, String word) {
        if (root == null) {
            return false;
        }
        if (word.length() == 0) {
            return root.isLeaf;
        }
        
        Map<Character, TrieNode> children = root.children;
        
        char c = word.charAt(0);
        if (c == '.') {
            for (char key : children.keySet()) {
                if (searchHelper(children.get(key), word.substring(1))) {
                    return true;
                }
            }
            return false;
        } else if (!children.containsKey(c)) {
            return false;
        } else {
            return searchHelper(children.get(c), word.substring(1));
        }
    }
}

// Your WordDictionary object will be instantiated and called as such:
// WordDictionary wordDictionary = new WordDictionary();
// wordDictionary.addWord("word");
// wordDictionary.search("pattern");
```