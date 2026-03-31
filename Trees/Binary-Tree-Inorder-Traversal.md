# Binary Tree Inorder Traversal

## 🟢 Problem
Given the root of a binary tree, return the inorder traversal of its nodes' values.

---

## 🧠 Understanding Inorder Traversal

Inorder traversal follows this order:

Left → Root → Right

Example:

        1
         \
          2
         /
        3

Inorder traversal: [1, 3, 2]

---

## 🚀 Approach 1: Recursive (DFS)

### Idea
- Traverse left subtree
- Visit root
- Traverse right subtree

### Code

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        inorder(root, result);
        return result;
    }

    private void inorder(TreeNode root, List<Integer> result) {
        if (root == null) return;

        inorder(root.left, result);   // Left
        result.add(root.val);         // Root
        inorder(root.right, result);  // Right
    }
}
```
🚀 Approach 2: Iterative (Using Stack)
Idea
Use a stack to simulate recursion
Go as left as possible first
Code
```
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode curr = root;

        while (curr != null || !stack.isEmpty()) {
            while (curr != null) {
                stack.push(curr);
                curr = curr.left;
            }

            curr = stack.pop();
            result.add(curr.val);
            curr = curr.right;
        }

        return result;
    }
}
```
⏱️ Complexity Analysis
Approach	Time Complexity	Space Complexity
Recursive	O(n)	O(h)
Iterative	O(n)	O(h)
n = number of nodes
h = height of tree