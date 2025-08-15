# [买卖股票的最佳时机III](买卖股票的最佳时机III"[题目地址](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/description/)")

## 题目描述

给定一个数组，它的第 i 个元素是一支给定的股票在第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 两笔 交易。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

### 思路：动态规划🌟


```java
class Solution {
    public int maxProfit(int[] prices) {
        // 最多两次交易——不交易/交易一次/交易两次——取最大利润
        if(prices.length <= 1) return 0;

        int buy1 = -prices[0]; // 第一次买入持有时 收益
        int sell1 = 0; // 第一次卖出 利润
        int buy2 = Integer.MIN_VALUE; // 第二次买入持有时 收益
        int sell2 = 0; // 第二次卖出 利润

        for(int i = 1; i < prices.length; i++){
            buy1 = Math.max(buy1, -prices[i]); // 第一次买：保持买入 或 重新买入
            sell1 = Math.max(buy1 + prices[i], sell1); // 第一次卖：第一次卖 或 不卖
            buy2 = Math.max(buy2, sell1 - prices[i]); // 第二次买：第一次卖后 - 今天的价
            sell2 = Math.max(sell2, buy2 + prices[i]); // 第一次卖：第二次卖 或 不卖
        }

        return sell2;
    }
}
```

#### 复杂度分析
时间复杂度：O(n)

空间复杂度：O(1)

### 总结
