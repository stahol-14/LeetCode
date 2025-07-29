# [组合总和II](组合总和II"[题目地址](https://leetcode.cn/problems/combination-sum-ii/description/)")

## 题目描述
给定一个候选人编号的集合 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的每个数字在每个组合中只能使用 一次 。

注意：解集不能包含重复的组合。 

### 思路：回溯

- candidates数组中可以有重复数字
- 每个数只能使用一次 ==〉 **去重**
- 为了方便去重，对数组进行排序


```java
class Solution {

    List<List<Integer>> result = new ArrayList<>();
    List<Integer> path = new ArrayList<>();

    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates); // 便于剪枝和去重
        backtracking(candidates, target, 0);
        return result;
    }

    private void backtracking(int[] candidates, int target, int start){
        // if(target < 0) return ;

        if(target == 0){
            result.add(new ArrayList<>(path));
            return ;
        }

        for(int i = start; i < candidates.length; i++){
            if(target - candidates[i] < 0) break; // 剪枝——需要对数组进行排序
            
            // 去重：同一层级中相同元素只处理一次（关键）
            if (i > start && candidates[i] == candidates[i - 1]) continue;

            path.add(candidates[i]);
            backtracking(candidates, target - candidates[i], i + 1); // 每个数字只能用一次
            path.remove(path.size() - 1);
        }
    }
}
```

#### 复杂度分析
时间复杂度：
空间复杂度：

### 总结
