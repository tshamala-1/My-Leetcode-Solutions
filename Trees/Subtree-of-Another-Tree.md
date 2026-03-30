Subtree of Another Tree
📘 Problem

Given the roots of two binary trees root and subRoot, return true if there is a subtree of root with the same structure and node values of subRoot and false otherwise.

A subtree of a binary tree is a tree that consists of a node in the tree and all of its descendants. A tree can also be considered a subtree of itself.

💡 Intuition
We traverse every node in the main tree (root)
At each node, we check:
Is this subtree identical to subRoot?
If yes → return true
Otherwise → recursively check left and right subtrees
🧠 Approach
Use a helper function isSameTree to compare two trees
Traverse the main tree
At each node:
If values match → check full subtree match
Else → continue searching
✅ Solution (Java)
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */

class Solution {
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if (root == null) return false;

        if (isSameTree(root, subRoot)) return true;

        return isSubtree(root.left, subRoot) || 
               isSubtree(root.right, subRoot);
    }

    private boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;

        if (p == null || q == null) return false;

        if (p.val != q.val) return false;

        return isSameTree(p.left, q.left) &&
               isSameTree(p.right, q.right);
    }
}
```
⏱️ Complexity Analysis
Time Complexity:
O(m * n)
m = nodes in root
n = nodes in subRoot
Space Complexity:
O(h) (recursion stack)
h = height of tree