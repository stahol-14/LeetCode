# [跳跃游戏II](跳跃游戏II"[题目地址](https://leetcode.cn/problems/jump-game-ii/description/)")

## 题目描述
给定一个长度为 n 的 0 索引整数数组 nums。初始位置为 nums[0]。

每个元素 nums[i] 表示从索引 i 向后跳转的最大长度。换句话说，如果你在 nums[i] 处，你可以跳转到任意 nums[i + j] 处:
- 0 <= j <= nums[i]
- i + j < n

返回到达 nums[n - 1] 的最小跳跃次数。生成的测试用例可以到达 nums[n - 1]。

### 思路：贪心
- 最少跳几次跳到最后
注意：
- 返回的是：从 0 跳到最后一个位置（n-1）所需的最小跳跃次数
  1. 因此 最后一个位置不需要达到 
  2. 否则 会多计算一次

```java
class Solution {
    public int jump(int[] nums) {
        int count = 0; // 跳跃次数
        int maxCover = 0; // 当前跳跃的边界：本次跳跃最多能跳到哪
        int curCover = 0; // 当前遍历过程中能跳到的最远位置（下一跳的覆盖范围）

        // 返回的是：从 0 跳到最后一个位置（n-1）所需的最小跳跃次数
        for(int i = 0; i < nums.length - 1; i++){ // 1. 因此 最后一个位置不需要达到 
            // 先计算 可以跳到的范围
            maxCover = Math.max(maxCover, i + nums[i]);

            // 再计算 处于当前范围边界 需要再次跳跃
            if(i == curCover){ // 2. 否则 会多计算一次
                count++;
                curCover = maxCover; // 更新范围
            }
        }

        return count;
    }
}
```

#### 复杂度分析
时间复杂度：O(n)
空间复杂度：O(1)

### 总结
