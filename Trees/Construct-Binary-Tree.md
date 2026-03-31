## Construct Binary Tree from Preorder and Inorder Traversal
🧩 Problem

Given two integer arrays preorder and inorder where:

preorder is the preorder traversal of a binary tree (Root → Left → Right)
inorder is the inorder traversal of the same tree (Left → Root → Right)

Construct and return the binary tree.

🧠 Approach
🔑 Key Observations
Preorder gives the root
First element in preorder is always the root
Inorder splits the tree
Elements left of root → left subtree
Elements right of root → right subtree
🚀 Strategy
Use a pointer preIndex to track current root in preorder

Use a HashMap to store:

value → index in inorder
Recursively:
Pick root from preorder
Find its index in inorder
Build left subtree
Build right subtree
⚙️ Algorithm Steps
Build a hashmap from inorder for quick lookup
Start recursion with full inorder range
At each step:
Create root from preorder
Split inorder using hashmap index
Recursively build left and right
💻 Code (Java)
```
class Solution {

    int preIndex = 0;
    HashMap<Integer, Integer> map = new HashMap<>();

    public TreeNode buildTree(int[] preorder, int[] inorder) {

        // Step 1: Store inorder value → index
        for (int i = 0; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }

        // Step 2: Build tree
        return helper(preorder, 0, inorder.length - 1);
    }

    private TreeNode helper(int[] preorder, int left, int right) {

        // Base case
        if (left > right) return null;

        // Step 3: Pick root from preorder
        int rootVal = preorder[preIndex++];
        TreeNode root = new TreeNode(rootVal);

        // Step 4: Find root in inorder
        int mid = map.get(rootVal);

        // Step 5: Build left subtree
        root.left = helper(preorder, left, mid - 1);

        // Step 6: Build right subtree
        root.right = helper(preorder, mid + 1, right);

        return root;
    }
}
```
⏱ Complexity
Time Complexity: O(n)
Space Complexity: O(n)