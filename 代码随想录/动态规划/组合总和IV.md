# [组合总和IV](组合总和IV"[题目地址](https://leetcode.cn/problems/combination-sum-iv/description/)")

## 题目描述
给你一个由 不同 整数组成的数组 nums ，和一个目标整数 target 。请你从 nums 中找出并返回总和为 target 的元素组合的个数。

题目数据保证答案符合 32 位整数范围。

### 思路：完全背包🌟（回溯）

注意：要找出来的是**排序数**——不同排序对应不同的结果

- 外层遍历目标和 `i = 0 ... target`，内层遍历每个数 num
- 转移：如果 i >= num，则把所有“凑到 i-num 的方案”在末尾再拼一个 num，得到和为 i 的方案：
  - `dp[i] += dp[i - num]`

```java
class Solution {
    public int combinationSum4(int[] nums, int target) {
        // 求出的组合 是排列数 即存在顺序
        int[] dp = new int[target + 1];
        dp[0] = 1;

        // 对于求排列——外层遍历背包，内层遍历物品
        for(int i = 1; i <= target; i++){
            for(int j = 0; j < nums.length; j++){
                if(i >= nums[j]){
                    // 当前目标整数 >= 当前数组值
                    dp[i] += dp[i - nums[j]]; // 在过去的基础上 加上当前值
                }
            }
        }

        return dp[target];
    }
}
```

#### 复杂度分析
时间复杂度：O(target * n)

空间复杂度：O(target)

### 总结
- 外层枚举金额，内层枚举数 —— 顺序敏感（排列）—— **外层背包，内层物品**