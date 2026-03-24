# Valid Anagram

## 🔹 Problem
Given two strings `s` and `t`, return `true` if `t` is an **anagram** of `s`, and `false` otherwise.  

**Examples:**  
- Input: `s = "anagram"`, `t = "nagaram"` → Output: `true`  
- Input: `s = "rat"`, `t = "car"` → Output: `false`

---

## 🔹 Intuition
Two strings are anagrams if they contain the same characters with the same frequency.  

We can solve this problem in **two ways**:  
1. **Sorting approach** – sort both strings and compare.  
2. **HashMap approach** – count the frequency of each character and compare counts.

---

## 🔹 Approach 1: Sorting
**Steps:**  
- If the lengths of `s` and `t` are different → return false.  
- Convert both strings to char arrays and sort them.  
- Compare the sorted arrays using `Arrays.equals()`.

### Code
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;

        char[] sArr = s.toCharArray();
        char[] tArr = t.toCharArray();

        Arrays.sort(sArr);
        Arrays.sort(tArr);

        return Arrays.equals(sArr, tArr);
    }
}

Time Complexity: O(n log n) (sorting)
Space Complexity: O(n) (for char arrays)

🔹 Approach 2: HashMap

Steps:

If lengths differ → return false.
Use a HashMap to count each character in s.
Iterate through t, decrement counts for each character.
If a character is missing or count goes below 0 → return false.
Otherwise → return true.
Code
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;

        Map<Character, Integer> count = new HashMap<>();

        for (char c : s.toCharArray()) {
            count.put(c, count.getOrDefault(c, 0) + 1);
        }

        for (char c : t.toCharArray()) {
            if (!count.containsKey(c)) return false;
            count.put(c, count.get(c) - 1);
            if (count.get(c) < 0) return false;
        }

        return true;
    }
}

Time Complexity: O(n)
Space Complexity: O(n) (for the HashMap)
