# [买卖股票的最佳时机IV](买卖股票的最佳时机IV"[题目地址](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/submissions/568774154/)")

## 题目描述
给你一个整数数组 prices 和一个整数 k ，其中 prices[i] 是某支给定的股票在第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 k 笔交易。也就是说，你最多可以买 k 次，卖 k 次。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

### 思路：动态规划🌟

- 当k大于n/2时，可以优化（n为数组长度）

外层“天数”、内层“状态从 1 到 2k 递增：
- 同一天里，允许“先用今天的价买入（更新奇数位）—— 再用今天的价卖出（更新偶数位）

```java
class Solution {
    public int maxProfit(int k, int[] prices) {
        int n = prices.length;
        if(n <= 1 || k == 0) return 0;

        // 如果 k >= n/2 则可以优化 ==> 累加正收益即可
        if(k > n / 2){
            int sum = 0;
            for(int i = 1; i < n; i++){
                if(prices[i] > prices[i - 1]){
                    sum += prices[i] - prices[i - 1];
                }
            }
            return sum;
        }

        // 使用动态规划 计算利润 —— 涉及到k次，需要使用数组
        int[] dp = new int[2 * k + 1]; // k为奇数 买入，k为偶数 卖出

        // 对dp数组进行初始化
        for(int i = 1; i <= 2 * k; i++){
            if(i % 2 == 1){
                dp[i] = -prices[0];
            }
        }

        // 开始买卖股票
        for(int i = 1; i < n; i++){ // i对应的是天数
            for(int j = 1; j <= 2 * k; j++){ // j对应的是买入状态——奇数买入/偶数卖出
                if(j % 2 == 1){
                    // 保持买入 或 重新买入
                    dp[j] = Math.max(dp[j], dp[j - 1] - prices[i]); 
                }else{
                    // 保持卖出 或 今天卖出
                    dp[j] = Math.max(dp[j], dp[j - 1] + prices[i]); 
                }
            }
        }

        return dp[2 * k];
    }
}
```

#### 复杂度分析
时间复杂度：O(n * k)

空间复杂度：O(k)

### 总结
