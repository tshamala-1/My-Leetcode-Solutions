# Maximum Depth of Binary Tree

## 🧩 Problem
Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

---

## 🌳 Example

    3
   / \
  9   20
     /  \
    15   7

**Output:**  

3


---

## 🧠 Intuition

- At each node, we want to know:
  - How deep is the left subtree?
  - How deep is the right subtree?
- Then we take the maximum of both and add 1 (for the current node)

👉 Each node asks:  
**"What is the maximum depth of my children?"**

---

## 🚀 Approach (DFS - Recursion)

### Steps:
1. If the node is `null`, return `0`
2. Recursively find:
   - Left subtree depth
   - Right subtree depth
3. Return:

1 + max(leftDepth, rightDepth)


---

## 💻 Code (Java)

```java
class Solution {
 public int maxDepth(TreeNode root) {
     if (root == null) return 0;

     int left = maxDepth(root.left);
     int right = maxDepth(root.right);

     return 1 + Math.max(left, right);
 }
}
🔍 Dry Run

For tree:

        1
       / \
      2   3
     /
    4
maxDepth(4) = 1
maxDepth(2) = 1 + max(1, 0) = 2
maxDepth(3) = 1
maxDepth(1) = 1 + max(2, 1) = 3
⏱️ Complexity
Time Complexity: O(n)
→ We visit every node once
Space Complexity: O(h)
→ Recursion stack (height of tree)
