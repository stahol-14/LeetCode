# [零钱兑换II](零钱兑换II"[题目地址](https://leetcode.cn/problems/coin-change-ii/description/)")

## 题目描述
给你一个整数数组 coins 表示不同面额的硬币，另给一个整数 amount 表示总金额。

请你计算并返回可以凑成总金额的硬币组合数。如果任何硬币组合都无法凑出总金额，返回 0 。

假设每一种面额的硬币有无限个。 

题目数据保证结果符合 32 位带符号整数。

### 思路：完全背包🌟

注意：要找出来的是**组合数**——无关排序

```java
class Solution {
    public int change(int amount, int[] coins) {

        int[] dp = new int[amount + 1]; // dp[j]：凑成金额 j 的组合数
        dp[0] = 1; // 凑成 0 的方法只有 1 种——什么都不选

        for(int i = 0; i < coins.length; i++){
            for(int j = coins[i]; j<= amount; j++){
                dp[j] += dp[j - coins[i]];
            }
        }
        return dp[amount];
    }
}
```

#### 复杂度分析
时间复杂度：O(amount * n)，n为coins数组的长度

空间复杂度：O(amount)

### 总结
- 外层枚举硬币，内层金额正序 —— 顺序不敏感（组合）—— **外层物品，内层背包**