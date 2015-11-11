# Encode and Decode Strings

[Leetcode](https://leetcode.com/problems/encode-and-decode-strings/)

題意：

Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.

Machine 1 (sender) has the function:
```
string encode(vector<string> strs) {
  // ... your code
  return encoded_string;
}
```
Machine 2 (receiver) has the function:
```
vector<string> decode(string s) {
  //... your code
  return strs;
}
```
So Machine 1 does:
```
string encoded_string = encode(strs);
```
and Machine 2 does:
```
vector<string> strs2 = decode(encoded_string);
```
strs2 in Machine 2 should be the same as strs in Machine 1.

Implement the encode and decode methods.

Note:
The string may contain any possible characters out of 256 valid ascii characters. Your algorithm should be generalized enough to work on any possible characters.
Do not use class member/global/static variables to store states. Your encode and decode algorithms should be stateless.
Do not rely on any library method such as eval or serialize methods. You should implement your own encode/decode algorithm.

解題思路：

> Pattern：stringLength + "/" + string

```java
public class Codec {

    // Encodes a list of strings to a single string.
    public String encode(List<String> strs) {
        StringBuilder sb = new StringBuilder();
        for (String str : strs) {
            int len = (str == null) ? 0 : str.length();;
            sb.append(len);
            sb.append("/");
            sb.append(str);
        }
        
        return sb.toString();
    }

    // Decodes a single string to a list of strings.
    public List<String> decode(String s) {
        List<String> res = new ArrayList<String>();
        
        int i = 0;
        while (i < s.length()) {
            int slashPosition = s.indexOf("/", i);
            int size = Integer.parseInt(s.substring(i, slashPosition));
            String value = s.substring(slashPosition + 1, slashPosition + size + 1);
            res.add(value);
            i = slashPosition + size + 1;
        }
        
        return res;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(strs));
```

---
###Reference
1. https://leetcode.com/discuss/55020/ac-java-solution