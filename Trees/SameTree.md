Same Tree

## 🟢 Problem
Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if:
- They are structurally identical
- The nodes have the same value

---

## 💡 Intuition
We compare both trees node by node:
- If both nodes are `null` → return true
- If only one is `null` → return false
- If values are different → return false
- Otherwise, recursively check left and right subtrees

---

## 🧠 Approach (Recursion / DFS)

We perform a depth-first traversal on both trees simultaneously.

---

## 🧾 Java Solution

```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {

        // both null → same
        if (p == null && q == null) return true;

        // one is null → not same
        if (p == null || q == null) return false;

        // values differ → not same
        if (p.val != q.val) return false;

        // check left and right subtrees
        return isSameTree(p.left, q.left) &&
               isSameTree(p.right, q.right);
    }
}

```
⏱ Complexity Analysis
Time Complexity: O(n)
→ Every node is visited once
Space Complexity: O(h)
→ Recursion stack (h = height of tree)