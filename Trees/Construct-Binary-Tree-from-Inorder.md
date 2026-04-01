Construct Binary Tree from Inorder and Postorder Traversal

🧩 Problem

Given two integer arrays inorder and postorder where:

inorder = Left → Root → Right
postorder = Left → Right → Root

Construct and return the binary tree.

🧠 Intuition
Postorder gives the root
The last element is always the root.
Inorder splits the tree
Elements left of root → left subtree
Elements right of root → right subtree
Important Order

Since we process postorder from the end:

root → right → left
So we must build right subtree first, then left.
✨ Example
inorder   = [9, 3, 15, 20, 7]
postorder = [9, 15, 7, 20, 3]

Tree:

        3
       / \
      9   20
         /  \
        15   7
💻 Java Solution
```
class Solution {
    int postIndex;
    HashMap<Integer, Integer> map = new HashMap<>();

    public TreeNode buildTree(int[] inorder, int[] postorder) {
        postIndex = postorder.length - 1;

        // Store inorder value -> index
        for (int i = 0; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }

        return helper(inorder, postorder, 0, inorder.length - 1);
    }

    private TreeNode helper(int[] inorder, int[] postorder, int left, int right) {
        if (left > right) return null;

        // Step 1: Pick root from postorder
        int rootVal = postorder[postIndex--];
        TreeNode root = new TreeNode(rootVal);

        // Step 2: Find root in inorder
        int index = map.get(rootVal);

        // Step 3: Build RIGHT subtree first
        root.right = helper(inorder, postorder, index + 1, right);

        // Step 4: Build LEFT subtree
        root.left = helper(inorder, postorder, left, index - 1);

        return root;
    }
}
```
⏱️ Complexity
Time: O(n)
Space: O(n)