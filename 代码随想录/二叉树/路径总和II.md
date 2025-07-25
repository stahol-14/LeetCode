# [路径总和II](路径总和II"[题目地址](https://leetcode.cn/problems/path-sum-ii/)")

## 题目描述
给你二叉树的根节点`root`和一个整数目标和  `targetSum`，找出所有**从根节点到叶子节点**路径总和等于给定目标和的路径。


### 思路：递归 + 回溯🌟
- 使用 `DFS` + 回溯 来遍历所有路径；
- 使用一个`path`列表临时记录当前路径；
- 到达 **叶子节点** 且路径和等于`targetSum`时，将路径加入结果列表
- 每次递归返回时进行回溯，保持路径正确

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
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> path = new ArrayList<>();

        dfs(root, targetSum, path, result);

        return result;
    }

    private void dfs(TreeNode node, int remainSum, List<Integer> path, List<List<Integer>> result) {
        if (node == null) return;

        path.add(node.val);  // 添加当前节点到路径中
        remainSum -= node.val;

        // 判断是否为叶子节点，且路径和等于目标和
        if (node.left == null && node.right == null && remainSum == 0) {
            result.add(new ArrayList<>(path));  // 必须 new 一个新 List 加入结果
        }

        // 递归左右子树
        dfs(node.left, remainSum, path, result);
        dfs(node.right, remainSum, path, result);

        // 回溯，撤销当前节点
        path.remove(path.size() - 1);
    }
}
```

#### 复杂度分析
时间复杂度：O(N)
空间复杂度：O(N)

### 总结