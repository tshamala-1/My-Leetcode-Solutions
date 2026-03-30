Serialize and Deserialize Binary Tree
🧩 Problem

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored or transmitted and reconstructed later.

Design an algorithm to:

Serialize a binary tree into a string
Deserialize the string back into the original tree
💡 Approach (BFS - Level Order Traversal)

We use Level Order Traversal (BFS) to ensure that the structure of the tree is preserved.

🔹 Key Idea
Store null nodes explicitly to maintain structure
Use a queue for traversal and reconstruction
✍️ Serialization (Tree → String)
Steps:
Use a queue and start from root
Traverse level by level
If node exists → append value
If node is null → append "null"
Example:
    1
   / \
  2   3
     / \
    4   5

Serialized Output:

"1,2,3,null,null,4,5,null,null,null,null"
🔁 Deserialization (String → Tree)
Steps:
Split string using ,
Create root node
Use queue to rebuild tree
Assign left and right children sequentially

✅ Java Implementation
```
public class Codec {

    // Serialize (Tree -> String)
    public String serialize(TreeNode root) {
        if (root == null) return "";

        StringBuilder sb = new StringBuilder();
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();

            if (node == null) {
                sb.append("null,");
            } else {
                sb.append(node.val).append(",");
                queue.offer(node.left);
                queue.offer(node.right);
            }
        }

        return sb.toString();
    }

    // Deserialize (String -> Tree)
    public TreeNode deserialize(String data) {
        if (data == null || data.isEmpty()) return null;

        String[] values = data.split(",");
        TreeNode root = new TreeNode(Integer.parseInt(values[0]));

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        int i = 1;

        while (!queue.isEmpty()) {
            TreeNode parent = queue.poll();

            // Left child
            if (!values[i].equals("null")) {
                TreeNode left = new TreeNode(Integer.parseInt(values[i]));
                parent.left = left;
                queue.offer(left);
            }
            i++;

            // Right child
            if (!values[i].equals("null")) {
                TreeNode right = new TreeNode(Integer.parseInt(values[i]));
                parent.right = right;
                queue.offer(right);
            }
            i++;
        }

        return root;
    }
}
```
🧠 Key Points
Always store "null" to preserve structure
BFS ensures correct reconstruction order
Queue is used in both serialization and deserialization
⏱️ Complexity
Operation	Time Complexity	Space Complexity
Serialize	O(n)	O(n)
Deserialize	O(n)	O(n)