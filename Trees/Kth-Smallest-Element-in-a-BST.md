Kth Smallest Element in a BST
🧩 Problem

Given the root of a Binary Search Tree (BST) and an integer k, return the kth smallest element (1-indexed).

💡 Key Idea
In a BST:
Left subtree < Root < Right subtree
Inorder traversal (Left → Root → Right) gives values in sorted order

👉 So, the kth element in inorder traversal = kth smallest element

🌳 Example
        5
       / \
      3   6
     / \
    2   4
   /
  1
Inorder Traversal:
1, 2, 3, 4, 5, 6

If k = 3,
👉 Output = 3

🔁 Approach: Inorder Traversal (Recursive)
Java Code
```
class Solution {
    int count = 0;
    int result = -1;

    public int kthSmallest(TreeNode root, int k) {
        inorder(root, k);
        return result;
    }

    private void inorder(TreeNode root, int k) {
        if (root == null) return;

        inorder(root.left, k);

        count++;
        if (count == k) {
            result = root.val;
            return;
        }

        inorder(root.right, k);
    }
}
```
🧠 How It Works (Step-by-Step)

We traverse the tree in inorder fashion:

Call Flow:
inorder(5)
 → inorder(3)
   → inorder(2)
     → inorder(1)
Visit Order:
Node	Count	Action
1	1	continue
2	2	continue
3	3	✅ found kth

👉 When count == k, we store the result.

⚠️ Important Note
return only exits the current function call
Recursion may continue in other branches
But since result is already found, it doesn't affect correctness
⚡ Optimized Version

To stop unnecessary traversal:
```

private void inorder(TreeNode root, int k) {
    if (root == null || count >= k) return;

    inorder(root.left, k);

    count++;
    if (count == k) {
        result = root.val;
        return;
    }

    inorder(root.right, k);
}
```
⏱ Complexity
Time: O(H + k)
Space: O(H) (recursion stack)