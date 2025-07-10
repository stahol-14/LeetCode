# [螺旋矩阵II](螺旋矩阵II"[题目地址](https://leetcode.cn/problems/spiral-matrix-ii/description/)")

## 题目描述
给你一个正整数 `n`，生成一个包含 `1` 到 `n²` 所有元素的、**元素按顺时针顺序螺旋排列的 `n x n` 正方形矩阵** `matrix`。

### 思路：直接模拟
定义四个边界变量：
- `left`、`right` 表示当前填充矩阵的左右边界；
- `top`、`bottom` 表示上下边界。

依次执行四个步骤（按顺时针）：
1. 从左到右填一行（`top` 行），然后 `top++`
2. 从上到下填一列（`right` 列），然后 `right--`
3. 从右到左填一行（`bottom` 行），然后 `bottom--`
4. 从下到上填一列（`left` 列），然后 `left++`

重复上述过程，直到所有数字填完为止。


```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] res = new int[n][n];
        int left = 0, right = n - 1;
        int top = 0, bottom = n - 1;
        int count = 1, target = n * n;

        while (count <= target) {
            // 从左到右
            for (int j = left; j <= right; j++) {
                res[top][j] = count++;
            }
            top++;
            // 从上到下
            for (int i = top; i <= bottom; i++) {
                res[i][right] = count++;
            }
            right--;
            // 从右到左
            for (int j = right; j >= left; j--) {
                res[bottom][j] = count++;
            }
            bottom--;
            // 从下到上
            for (int i = bottom; i >= top; i--) {
                res[i][left] = count++;
            }
            left++;
        }

        return res;
    }
}
```

#### 复杂度分析
时间复杂度：O(n^2)
空间复杂度：O(n^2)

### 总结
需要注意边界条件，【循环不变量原则】