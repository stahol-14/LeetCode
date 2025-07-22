# [二叉树的层序遍历II](二叉树的层序遍历II"[题目地址](https://leetcode.cn/problems/binary-tree-level-order-traversal-ii/description/)")

## 题目描述
给你二叉树的根节点`root`，返回其节点值**自底向上**的层序遍历。（即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

### 思路1：层序遍历+反转（迭代）


```java
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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) return res;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while(!queue.isEmpty()){
            int levelSize = queue.size();
            List<Integer> level = new ArrayList<>();

            for(int i = 0; i < levelSize; i++){
                TreeNode node = queue.poll();
                level.add(node.val);

                if(node.left != null) queue.offer(node.left);
                if(node.right != null) queue.offer(node.right);
            }
            res.add(level);
        }

        Collections.reverse(res);
        return res;
    }
}
```

#### 复杂度分析
时间复杂度：O(n)
空间复杂度：O(n)

----

### 思路2：层序遍历(双向链表+头插法)


```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        LinkedList<List<Integer>> res = new LinkedList<>(); // 用 LinkedList 支持头插
        if (root == null) return res;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root); // 从根节点开始 BFS

        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> level = new ArrayList<>();

            // 遍历当前层的所有节点
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                level.add(node.val);

                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }

            // 将这一层的结果插入到头部（区别于普通的 add）
            res.addFirst(level);
        }

        return res;
    }
}

```

#### 复杂度分析
时间复杂度：O(n)
空间复杂度：O(n)

### 总结