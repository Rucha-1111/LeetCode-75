# LeetCode 1768 – Merge Strings Alternately

**Difficulty:** Easy  
**Topics:** String, Two Pointers  

**Problem Link:** [1768 - Merge Strings Alternately](https://leetcode.com/problems/merge-strings-alternately/)

---

## Problem Statement

You are given two strings `word1` and `word2`.

Merge the strings by adding letters in **alternating order**, starting with `word1`.

If one string is longer than the other, append the **remaining letters** of the longer string to the end of the merged string.

Return the merged string.

---

## Examples

### Example 1
**Input:** `word1 = "abc"`, `word2 = "pqr"`  
**Output:** `"apbqcr"`  

### Example 2
**Input:** `word1 = "ab"`, `word2 = "pqrs"`  
**Output:** `"apbqrs"`  

---
## Java Solution 1 - Using StringBuilder
```java
class Solution {
    public String mergeAlternately(String word1, String word2) {
        StringBuilder result = new StringBuilder();
        StringBuilder sb = new StringBuilder();
        final int n = Math.min(word1.length(), word2.length());

        for(int i = 0; i < n; i++) {
            sb.append(word1.charAt(i));
            sb.append(word2.charAt(i));
        }

        return sb.append(word1.substring(n)).append(word2.substring(n)).toString();
    }
}
```
- First we create the object *sb* of the **StringBuilder** class. *__StringBuilder__* is a dynamically resizable character buffer that allows in-place modification of text without creating new objects. But what does it actually mean?
- Basically when we create an object of a  **StringBuilder** class, **Java** creates an empty box or a container in the memory to store characters.
- When we append the characters to this object, they simply being placed in the same box. And if this box i.e., space gets full, Java simply creates more space automatically to store the characters. And all of this happens automatically.

* **Time Complexity:** $O(n + m)$
    * The loop runs $\min(n, m)$ times, performing constant time operations.
    * The `substring()` and `append()` operations at the end take time proportional to the number of remaining characters.
    * Every character in both input strings is processed exactly once.
* **Space Complexity:** $O(n + m)$
    * The `StringBuilder` stores the combined length of both strings.
    * While `substring()` creates new temporary string objects in Java, the total auxiliary space remains linear relative to the input size.

---
## Java Solution 2 - Using String
```java
class Solution {
    public String mergeAlternately(String word1, String word2) {
        final int n = Math.min(word1.length(), word2.length());
        String mergedString = "";

        for (int i = 0; i < n; i++) {
            mergedString += word1.charAt(i);
            mergedString += word2.charAt(i);
        }

        return mergedString + word1.substring(n) + word2.substring(n);
    }
}
```
- To merge two strings into one we have to first calculate the length of the **shortest string** so that we can run the loop till that length. 
- Upon receiving the minimum length, we run the loop through that string and retreive the first character from string 1 and then the first character from string 2.
- We repeat this process till the end of the shortest string and then we come out of the loop. 
- After that, we return the **mergedString** by adding the rest of the characters of the longer string to the **mergedString** using the *substring()* method.

* **Time Complexity:** $O((n + m)^2)$  
    * The loop runs $\min(n, m)$ times, but each `+=` operation on a `String` creates a **new String object** and copies existing characters.
    * As the string grows, every concatenation takes longer, leading to repeated copying.
    * The final concatenation with `substring()` also creates new String objects.
    * Due to repeated reallocations and copying, the overall time complexity becomes **quadratic** in the combined length of both strings.

* **Space Complexity:** $O(n + m)$  
    * The final merged string stores all characters from both input strings.
    * Multiple temporary String objects are created during concatenation, but they are discarded by the garbage collector.
    * The peak auxiliary space grows linearly with the total input size.


---

## Key Takeaways
Both the approaches solve the problem accurately and do produce the expected output, but their efficiency is to be taken into consideration. Using *Strings* in Java is inefficient since they create a new object for every concatenation, taking up a lot of space and causing unnecessary time overhead. 

Using **StringBuilder** eradicates the above issues as they modify the same object in the memory, avoiding repeated object creation, thereby making it more efficient and effective in scenarios of frequent operations. 


