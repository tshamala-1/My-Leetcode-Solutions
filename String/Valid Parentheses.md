# Valid Parentheses

## 🔹 Problem
Given a string s containing '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

---

## 🔹 Intuition
At first glance, we need to make sure:
- Every opening bracket has a matching closing bracket
- The order is correct

This reminds me of **LIFO (Last In First Out)** behavior → which is exactly how a **stack** works.

---

## 🔹 Approach
- Use a stack to store opening brackets
- Traverse each character:
  - If opening → push to stack
  - If closing:
    - Check if stack is empty → invalid
    - Pop and compare
- At the end → stack must be empty

---

## 🔹 Code (Java)
```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();

        for (char c : s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[') {
                stack.push(c);
            } else {
                if (stack.isEmpty()) return false;

                char top = stack.pop();
                if ((c == ')' && top != '(') ||
                    (c == '}' && top != '{') ||
                    (c == ']' && top != '[')) {
                    return false;
                }
            }
        }

        return stack.isEmpty();
    }
}
