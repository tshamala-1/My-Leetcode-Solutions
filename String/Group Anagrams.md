# Group Anagrams

## 🔹 Problem
Given an array of strings `strs`, group the anagrams together.  
You can return the answer in **any order**.

**Example:**  
Input: `["eat","tea","tan","ate","nat","bat"]`  
Output: `[["bat"],["nat","tan"],["ate","eat","tea"]]`

---

## 🔹 Intuition
Anagrams have the same characters in different orders.  
If we **sort the characters of each string**, all anagrams will produce the same sorted string.  
We can use this as a **key** in a HashMap to group them together.

---

## 🔹 Approach
1. Initialize a HashMap: `Map<String, List<String>>`  
   - Key → sorted string  
   - Value → list of original strings
2. For each string in the array:
   - Convert it to a char array and sort it
   - Convert back to a string → this is the **key**
   - Add the original string to the list in the map
3. At the end, return all values of the map as a list of lists.

---

## 🔹 Code (Java)
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap<>();

        for (String s : strs) {
            char[] arr = s.toCharArray();
            Arrays.sort(arr);
            String key = new String(arr);

            map.putIfAbsent(key, new ArrayList<>());
            map.get(key).add(s);
        }

        return new ArrayList<>(map.values());
    }
}
