# 🌳 Binary Tree Maximum Path Sum

## 🧩 Problem Statement

Given the root of a binary tree, return the **maximum path sum** of any non-empty path.

A path is a sequence of nodes where each pair of adjacent nodes is connected by an edge.  
A node can appear at most once in the path.

The path does **not need to pass through the root**.

---

## 💡 Key Idea

At every node, we consider two possibilities:

### 1. Path passing THROUGH the node
- left subtree + node + right subtree  
- This is used to update the global answer

### 2. Path going UP to parent
- node + max(left, right)  
- Only one side can be chosen (no branching allowed upward)

---

## ⚙️ Approach (DFS)

We use Depth First Search (postorder traversal):

- Compute left subtree max gain
- Compute right subtree max gain
- Ignore negative values (use 0 instead)
- Update global maximum
- Return best path going upward

---

## 🧠 Why ignore negatives?

If a path is negative, it will reduce the total sum.  
So we treat negative contributions as 0.

---

## 🚀 Java Solution

```java
class Solution {

    int maxSum = Integer.MIN_VALUE;

    public int maxPathSum(TreeNode root) {
        dfs(root);
        return maxSum;
    }

    private int dfs(TreeNode node) {
        if (node == null) return 0;

        int left = Math.max(0, dfs(node.left));
        int right = Math.max(0, dfs(node.right));

        // Path passing through current node
        int currentPath = node.val + left + right;

        // Update global maximum
        maxSum = Math.max(maxSum, currentPath);

        // Return best path going upward
        return node.val + Math.max(left, right);
    }
}
```

⏱ Complexity Analysis
Time Complexity: O(n) → every node visited once
Space Complexity: O(h) → recursion stack (h = height of tree)