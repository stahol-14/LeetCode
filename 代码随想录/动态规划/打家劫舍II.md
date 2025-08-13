# [打家劫舍II](打家劫舍II"[题目地址](https://leetcode.cn/problems/house-robber-ii/description/)")

## 题目描述
你是一个专业的小偷，计划偷窃沿街的房屋，每间房内都藏有一定的现金。这个地方所有的房屋都 围成一圈 ，这意味着第一个房屋和最后一个房屋是紧挨着的。同时，相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警 。

给定一个代表每个房屋存放金额的非负整数数组，计算你 在不触动警报装置的情况下 ，今晚能够偷窃到的最高金额。

### 思路：动态规划


```java
class Solution {
    public int rob(int[] nums) {
        // 因为首尾相连 构成了环 因此需要对长度进行判断
        // 奇数——从下标0到n-2  偶数——从下标1到n-1
        int n = nums.length;
        if (n == 1) return nums[0];
        if (n == 2) return Math.max(nums[0], nums[1]);

        // 情况 A：考虑 [0, n-2]
        int a = robRange(nums, 0, n - 2);
        // 情况 B：考虑 [1, n-1]
        int b = robRange(nums, 1, n - 1);

        return Math.max(a, b);
    }

    private int robRange(int[] nums, int start, int end){
        int prev2 = 0; // dp[i-2]
        int prev1 = 0; // dp[i-1]

        for(int i = start; i <= end; i++){
            int curr = Math.max(prev1, prev2 + nums[i]); // 当前房屋
            prev2 = prev1;
            prev1 = curr;
        }

        return prev1;
    }
}
```

#### 复杂度分析
时间复杂度：O(n)

空间复杂度：O(n)

### 总结
