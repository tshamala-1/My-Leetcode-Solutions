# ✅ Validate Binary Search Tree (BST)

## 📌 Problem Statement

Given the root of a binary tree, determine if it is a valid Binary Search Tree (BST).

A valid BST is defined as:

- The left subtree of a node contains only nodes with keys **strictly less** than the node's key.
- The right subtree of a node contains only nodes with keys **strictly greater** than the node's key.
- Both left and right subtrees must also be valid BSTs.

---

## 🧠 Key Insight

A BST is not just about comparing a node with its immediate children.

👉 Every node must satisfy constraints from **all its ancestors**.

So instead of simple comparisons, we use a **range-based approach**:

- Each node must lie within a valid range: `(min, max)`
- This range gets updated as we move down the tree.

---

## 🔁 Approach: Range Validation (DFS)

### Idea:

- Start with range: `(-∞, +∞)`
- For each node:
  - Check if it lies within the valid range
  - Recursively validate left and right subtrees with updated ranges

---

## ⚙️ Algorithm

1. Start from root with range `(Long.MIN_VALUE, Long.MAX_VALUE)`
2. If node is `null`, return `true`
3. If `node.val` is not in `(min, max)`, return `false`
4. Recursively:
   - Left → `(min, node.val)`
   - Right → `(node.val, max)`

---

## 💻 Java Solution

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        return validate(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean validate(TreeNode node, long min, long max) {
        if (node == null) return true;

        if (node.val <= min || node.val >= max) return false;

        return validate(node.left, min, node.val) &&
               validate(node.right, node.val, max);
    }
}
```

⏱️ Complexity Analysis
Time Complexity:
O(n) → Every node is visited once
Space Complexity:
O(h) → Recursion stack (h = height of tree)