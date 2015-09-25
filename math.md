#Cosine Similarity

[]()

題意：

Cosine similarity is a measure of similarity between two vectors of an inner product space that measures the cosine of the angle between them. The cosine of 0° is 1, and it is less than 1 for any other angle.

See wiki: [Cosine Similarity](https://en.wikipedia.org/wiki/Cosine_similarity)

Given two vectors A and B with the same size, calculate the cosine similarity.

Return 2.0000 if cosine similarity is invalid (for example A = [0] and B = [0]).

Have you met this question in a real interview? Yes
Example
Given A = [1, 2, 3], B = [2, 3 ,4].

Return 0.9926.

Given A = [0], B = [0].

Return 2.0000

解題思路：

水題，照著 wiki上的公式直接寫即可，程式碼如下：

```java
public class Solution {
    /**
     * @param A an integer array
     * @return  A list of integers includes the index of the first number and the index of the last number
     */
    public ArrayList<Integer> continuousSubarraySumII(int[] A) {
        
        ArrayList<Integer> res = new ArrayList<Integer>();
        if (A == null || A.length == 0) {
            return res;
        }
        
        int start = 0;
        int end = 0;
        int sum = A[0];
        int max = A[0];
        int totalSum = A[0];
        res.add(0);
        res.add(0);
        
        for (int i = 1; i < A.length; i++) {
            if (sum < 0) {
                start = i;
                sum = A[i];
            } else {
                sum += A[i];
            }
            end = i;
            
            if (sum > max) {
                max = sum;
                res.set(0, start);
                res.set(1, end);
            }
            
            totalSum += A[i]; // for latter use.
        }
        
        int[] negativeA = new int[A.length];
        for (int i = 0; i < A.length; i++) {
            negativeA[i] = -A[i];
        }
        
        start = 0;
        end = 0;
        sum = negativeA[0];
        for (int i = 1; i < negativeA.length; i++) {
            if (sum < 0) {
                start = i;
                sum = negativeA[i];
            } else {
                sum += negativeA[i];
            }
            end = i;
            
            if (totalSum + sum > max) {
                max = totalSum + sum;
                res.set(0, end + 1);
                res.set(1, start - 1);
            }
        }
        
        return res;
        
        
        
    }
}
```