# [最后一块石头的重量II](最后一块石头的重量II"[题目地址](https://leetcode.cn/problems/last-stone-weight-ii/description/)")

## 题目描述
有一堆石头，用整数数组 stones 表示。其中 stones[i] 表示第 i 块石头的重量。

每一回合，从中选出任意两块石头，然后将它们一起粉碎。假设石头的重量分别为 x 和 y，且 x <= y。那么粉碎的可能结果如下：

- 如果 x == y，那么两块石头都会被完全粉碎；
- 如果 x != y，那么重量为 x 的石头将会完全粉碎，而重量为 y 的石头新重量为 y-x。
 
最后，最多只会剩下一块 石头。返回此石头 最小的可能重量 。如果没有石头剩下，就返回 0。

### 思路：0/1 背包（一维）

注意：和为偶数不代表差值为0，可能拼不出来sum/2的大小

- 定义：dp[j] 表示不超过 j 能凑到的最大子集和
- 转移：对每个石头重量 w，倒序更新
  - `dp[j] = max(dp[j], dp[j-w] + w)（当 j >= w）`

```java
class Solution {
    public int lastStoneWeightII(int[] stones) {
        // 将石头均分为两部分 差值尽可能小
        int sum = 0;
        for(int w : stones){
            sum += w;
        }

        int target = sum / 2; // 目标是尽量选到接近 sum/2 的子集和
        int n = stones.length;
        int[] dp = new int[target + 1];

        for(int i = 0; i < n; i++){
            for(int j = target; j >= stones[i]; j--){
                // 先石头 再大小 —— 正向遍历 + 逆向遍历
                dp[j] = Math.max(dp[j], dp[j - stones[i]] + stones[i]);
            }
        }

        return sum - 2 * dp[target];
    }
}
```

#### 复杂度分析
时间复杂度：O(M * N)

空间复杂度：O(N)

### 总结
