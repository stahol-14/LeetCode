# [打家劫舍III](打家劫舍III"[题目地址](https://leetcode.cn/problems/house-robber-iii/description/)")

## 题目描述
小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为 root 。

除了 root 之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果 两个直接相连的房子在同一天晚上被打劫 ，房屋将自动报警。

给定二叉树的 root 。返回 在不触动警报的情况下 ，小偷能够盗取的最高金额 。

### 思路：dp + 后序遍历（左右根）🌟

- 相邻房子（父子）不能在同一晚偷

对任意结点 node，有两种状态：
- rob：偷这个结点时，能拿到的最大金额——只能加上两个孩子“不偷”的最优
`rob = node.val + left.notRob + right.notRob`
- notRob：不偷这个结点时，能拿到的最大金额——每个孩子可偷可不偷，取最大
`notRob = max(left.rob, left.notRob) + max(right.rob, right.notRob)`

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
    public int rob(TreeNode root) {
        int[] res = dfs(root);
        return Math.max(res[0], res[1]);
    }

    // 返回长度为 2 的数组 res：
    // res[0] = rob，表示偷当前结点的最大金额
    // res[1] = notRob，表示不偷当前结点的最大金额
    private int[] dfs(TreeNode root){
        // 后序遍历（左 右 根）
        int[] res = new int[2];
        if(root == null) return res;

        // 遍历左右子树
        int[] left = dfs(root.left);
        int[] right = dfs(root.right);

        // 处理当前节点
        // res[0] 偷当前节点 —— 左右孩子都不偷
        // res[1] 不偷当前节点 —— 左右孩子 偷不偷取决于他们当前的最大值
        res[0] = root.val + left[1] + right[1];
        res[1] = Math.max(left[0], left[1]) + Math.max(right[0], right[1]);

        return res;
    }
}
```

#### 复杂度分析
时间复杂度：O(n)，每个结点只访问一次

空间复杂度：O(h)，递归栈深度（h 为树高；最坏 O(n)，平均 O(log n)）

### 总结
