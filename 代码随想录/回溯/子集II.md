# [子集II](子集II"[题目地址](https://leetcode.cn/problems/subsets-ii/description/)")

## 题目描述
给你一个整数数组 nums ，其中可能包含重复元素，请你返回该数组所有可能的 子集（幂集）。

解集 不能 包含重复的子集。返回的解集中，子集可以按 任意顺序 排列。

### 思路

注：数组存在重复元素
- 因此：子集中可以存在重复元素但子集不能重复
- 需要去重——需要先排序

```java
class Solution {

    List<List<Integer>> result = new ArrayList<>();
    List<Integer> paths = new ArrayList<>();

    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        backtracking(nums, 0);
        return result;
    }

    private void backtracking(int[] nums, int start){
        result.add(new ArrayList<>(paths));

        if(start >= nums.length) return ;

        for(int i = start; i < nums.length; i++){
            // 如果在 这一层的筛选中 选过了该值 即重复，跳过
            if(i > start && nums[i] == nums[i - 1]){
                continue;
            }
            paths.add(nums[i]);
            backtracking(nums, i + 1); // 递归 从下一位开始找
            paths.remove(paths.size() - 1); // 回溯
        }
    }
}
```

#### 复杂度分析
时间复杂度：
空间复杂度：

### 总结
- 对于这道题目来说，子集中可以存在重复的数字，但是不能出现重复的子集，即：可以有[1, 2, 2],但不可以有[2],[2]两个相同的子集
- 因此，这个去重，是横向遍历时的去重，即：for循环时进行去重