# Longest Palindromic Substring

## Problem

Given a string `s`, return the **longest palindromic substring** in `s`.  

A **palindromic substring** reads the same forward and backward.

---

## Approach

We can solve this using the **expand-around-center** technique:

1. Every palindrome has a **center**, which can be:
   - A single character (odd-length palindrome)
   - Two consecutive characters (even-length palindrome)
2. For each index in the string:
   - Expand around it to find the longest odd-length palindrome
   - Expand around it and the next character to find the longest even-length palindrome
3. Keep track of the longest palindrome seen so far.
4. Return the longest substring at the end.

---

## Java Implementation

```java
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() < 1) return "";
        int start = 0, end = 0;

        for (int i = 0; i < s.length(); i++) {
            int len1 = expandAroundCenter(s, i, i);       // Odd-length
            int len2 = expandAroundCenter(s, i, i + 1);   // Even-length
            int len = Math.max(len1, len2);

            if (len > end - start) {
                start = i - (len - 1) / 2;
                end = i + len / 2;
            }
        }

        return s.substring(start, end + 1);
    }

    private int expandAroundCenter(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        return right - left - 1; // length of palindrome
    }
}
```
Complexity Analysis
Time Complexity: O(n²) — Each center is expanded at most n times
Space Complexity: O(1) — Only pointers and indices are used

Example 1:

Input: s = "babad"

Output: "bab"

Explanation: "aba" is also a valid answer.

Example 2:

Input: s = "cbbd"

Output: "bb


