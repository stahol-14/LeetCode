# [买卖股票的最佳时机II](买卖股票的最佳时机II"[题目地址](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/description/)")

## 题目描述
给你一个整数数组 prices ，其中 prices[i] 表示某支股票第 i 天的价格。

在每一天，你可以决定是否购买和/或出售股票。你在任何时候 最多 只能持有 一股 股票。你也可以先购买，然后在 同一天 出售。

返回 你能获得的 最大利润 。

### 思路：贪心


```java
class Solution {
    public int maxProfit(int[] prices) {
        // 贪心
        int profit = 0;
        if(prices.length <= 1) return profit;

        for(int i = 0; i < prices.length; i++){
            if(i > 0 && prices[i] > prices[i - 1]){
                profit += prices[i] - prices[i - 1];
            }
        }

        return profit;
    }
}
```

#### 复杂度分析
时间复杂度：O(n)

空间复杂度：O(1)

----

### 思路：dp


```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length <= 1) return 0;

        int dp0 = -prices[0]; // 持有时的利润
        int dp1 = 0; // 卖出后的最大收益

        for(int i = 1; i < prices.length; i++){
            dp0 = Math.max(dp1 - prices[i], dp0); // 今天买入 或 保持买入
            dp1 = Math.max(dp0 + prices[i], dp1); // 今天卖出 或 保持卖出
        }

        return dp1;
    }
}
```

#### 复杂度分析
时间复杂度：O(n)

空间复杂度：O(1)

### 总结
