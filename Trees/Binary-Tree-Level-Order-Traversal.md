# Binary Tree Level Order Traversal

## 🧩 Problem
Given the root of a binary tree, return the level order traversal of its nodes' values (i.e., from left to right, level by level).

---

## 🌳 Example


Input:
3
/
9 20
/
15 7

Output:
[[3],[9,20],[15,7]]


---

## 🧠 Intuition

- Use **Breadth-First Search (BFS)**.
- Traverse the tree level by level using a **queue**.
- Process all nodes at the current level before moving to the next.

---

## 🚀 Approach

1. Use a queue and add the root.
2. While queue is not empty:
   - Get the current level size.
   - Process exactly that many nodes.
   - Add their children to the queue.
3. Store each level in the result.

---

## 💻 Java Code

```java
import java.util.*;

class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            int levelsize = queue.size();
            List<Integer> level = new ArrayList<>();

            for (int i = 0; i < levelsize; i++) {
                TreeNode node = queue.poll();
                level.add(node.val);

                if (node.left != null) {
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }

            result.add(level);
        }
        return result;
    }
}

```
⏱ Complexity
Time: O(n)
Space: O(n)