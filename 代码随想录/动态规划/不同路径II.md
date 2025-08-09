# [不同路径II](不同路径II"[题目地址](https://leetcode.cn/problems/unique-paths-ii/description/)")

## 题目描述
给定一个 m x n 的整数数组 grid。一个机器人初始位于 左上角（即 grid[0][0]）。机器人尝试移动到 右下角（即 grid[m - 1][n - 1]）。机器人每次只能向下或者向右移动一步。

网格中的障碍物和空位置分别用 1 和 0 来表示。机器人的移动路径中不能包含 任何 有障碍物的方格。

返回机器人能够到达右下角的不同路径数量。

测试用例保证答案小于等于 2 * 10^9。

### 思路


```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        // 因为有障碍物 所以 在移动时增加一轮判断
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] dp = new int[m][n];

        // 进行初始化
        for(int i = 0; i < m; i++){
            if(obstacleGrid[i][0] == 1){
                break;
            }
            dp[i][0] = 1;
        }
        for(int j = 0; j < n; j++){
            if(obstacleGrid[0][j] == 1){
                break;
            }
            dp[0][j] = 1;
        }

        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                if(obstacleGrid[i][j] == 0){
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
                }
            }
        }

        return dp[m - 1][n - 1];
    }
}
```

#### 复杂度分析
时间复杂度：O(m * n)

空间复杂度：O(m * n)

### 总结
