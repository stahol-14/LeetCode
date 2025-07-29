# [组合总和III](组合总和III"[题目地址](https://leetcode.cn/problems/combination-sum-iii/description/)")

## 题目描述
找出所有相加之和为 n 的 k 个数的组合，且满足下列条件：
- 只使用数字 1 到 9
- 每个数字 **最多使用一次** 
- 返回 所有可能的有效组合的列表 。该列表**不包含重复组合**，组合可以以任何顺序返回。

### 思路：回溯
题意：闭区间[1, 9]找k个数，组成n

```java
class Solution {
    // 将 结果以及中间获得的组合 定义为全局变量，可以简化回溯函数的参数
    List<List<Integer>> result = new ArrayList<>();
    List<Integer> paths = new LinkedList<>();

    public List<List<Integer>> combinationSum3(int k, int n) {
        backtracking(k, n, 1); // 从1开始
        return result;
    }

    private void backtracking(int k, int targetSum,int start){
        if(targetSum < 0){ // 剪枝
            return ;
        }

        if(paths.size() == k && targetSum == 0){
            result.add(new ArrayList<>(paths));
            return ;
        }

        for(int i = start; i <= 9 - (k - paths.size()) + 1; i++){
            // targetSum -= i;
            paths.add(i);
            backtracking(k, targetSum - i, i + 1);
            paths.removeLast(); // 回溯
            // targetSum += i; // 回溯 把要求得和复原
        }
    }
}
```

#### 复杂度分析
时间复杂度：O(k * C(9, k))
空间复杂度：O(k)

### 总结
