# LeetCode 1768 – Merge Strings Alternately

**Difficulty:** Easy  
**Topics:** String, Two Pointers  

🔗 **Problem Link:** [https://leetcode.com/problems/merge-strings-alternately/](https://leetcode.com/problems/merge-strings-alternately/)

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

## Intuition & Logic

The problem asks us to "zip" two strings together. We iterate through both strings simultaneously. At each step, we take one character from the first string (if available) and then one from the second (if available).

---

## Approach: Min-Length & Suffix Appending

This approach optimizes the merging process by pre-calculating the overlapping boundary of the two strings to minimize conditional checks.

1.  **Find the Intersection:** Calculate $n = \min(\text{word1.length}, \text{word2.length})$. This represents the length where both strings are guaranteed to have characters.
2.  **Synchronized Loop:** Use a `for` loop from $0$ to $n$. In each iteration, append the $i$-th character of `word1` and then the $i$-th character of `word2` to a `StringBuilder`.
3.  **Direct Suffix Appending:** Instead of using pointers to find the remaining characters, use the `substring(n)` method on both strings:
    * If a string is longer than $n$, `substring(n)` extracts the remaining part.
    * If a string is length $n$, `substring(n)` returns an empty string (`""`), which has no impact when appended.
4.  **Efficiency:** This reduces the number of "if" statements executed during the main iteration.

---

## Complexity Analysis

* **Time Complexity:** $O(n + m)$
    * The loop runs $\min(n, m)$ times, performing constant time operations.
    * The `substring()` and `append()` operations at the end take time proportional to the number of remaining characters.
    * Every character in both input strings is processed exactly once.
* **Space Complexity:** $O(n + m)$
    * The `StringBuilder` stores the combined length of both strings.
    * While `substring()` creates new temporary string objects in Java, the total auxiliary space remains linear relative to the input size.

---
## Java Solution
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
