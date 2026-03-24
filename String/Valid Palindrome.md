# Valid Palindrome

## Problem

A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward.  

Alphanumeric characters include **letters and numbers**.  

**Task:** Given a string `s`, return `true` if it is a palindrome, otherwise return `false`.

---

## Approach

We can solve this using a **two-pointer approach**:

1. Initialize two pointers:  
   - `left` at the start of the string  
   - `right` at the end of the string
2. Move both pointers toward the center:
   - Skip any non-alphanumeric characters using `Character.isLetterOrDigit()`
3. Compare characters at both pointers (case-insensitive):
   - Convert characters to lowercase using `Character.toLowerCase()`
4. If any characters don't match, return `false`
5. If pointers cross without mismatches, return `true`

---

## Java Implementation

```java
class Solution {
    public boolean isPalindrome(String s) {
        if (s == null) return false;

        int left = 0;
        int right = s.length() - 1;

        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }

            if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) {
                return false;
            }

            left++;
            right--;
        }

        return true;
    }
}
```

Examples
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: After removing non-alphanumeric characters and converting to lowercase: 
"amanaplanacanalpanama" → reads the same forward and backward.

Input: s = "race a car"
Output: false
Explanation: After cleaning: "raceacar" → not a palindrome.
Complexity Analysis
Time Complexity: O(n) — Each character is visited at most once
Space Complexity: O(1) — Only two pointers are used

