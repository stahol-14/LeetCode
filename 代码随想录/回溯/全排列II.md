# [全排列II](全排列II"[题目地址](https://leetcode.cn/problems/permutations-ii/description/)")

## 题目描述
给定一个可包含重复数字的序列 nums ，按任意顺序 返回所有不重复的全排列。


### 思路🌟🌟

- 区别：可包含重复数字的序列 nums
- 直接计算得到的全排列可能存在重复数字，因此需要去重——排序
- 去重的逻辑是：如果在同一层中，遇到了重复的数字，且已经使用过了，则需要跳过

```java
class Solution {

    List<List<Integer>> result = new ArrayList<>();
    List<Integer> path = new ArrayList<>();

    public List<List<Integer>> permuteUnique(int[] nums) {
        Arrays.sort(nums);
        boolean[] used = new boolean[nums.length];
        backtracking(nums, used);
        return result;
    }

    private void backtracking(int[] nums, boolean[] used){

        // 全排列 长度相等时 加入到结果集
        if(path.size() == nums.length){
            result.add(new ArrayList<>(path));
            return ;
        }

        for(int i = 0; i < nums.length; i++){
            // 剪枝 当前层存在重复数值 如
            if(i > 0 && nums[i] == nums[i - 1] && used[i - 1] == false){
                continue;
            }

            if(!used[i]){
                // 使用并记录
                used[i] = true;
                path.add(nums[i]); 

                backtracking(nums, used); // 递归

                path.remove(path.size() - 1); // 回溯
                used[i] = false;
            }
            
        }
    }
}
```

#### 复杂度分析
时间复杂度：
空间复杂度：

### 总结
不同方式的去重逻辑：

- 树层去重：
  - 目标：得到不重复的结果集（如组合/排列），输入数组可能有重复元素。
  - 对于组合、排序来说，如果原数组中存在重复元素，那么为了获得**不重复的子集结果**，需要去重处理，去重的逻辑是：先对数组进行排序，然后在**同一层**中遇到重复值时，跳过。
  - 本质：就是在同一层的同一位置上，不取相同数字，从而实现去重。


- 树枝去重：
  - 目标：找出满足约束的子序列（如递增子序列），元素不能乱序。
  - 对于子序列来说，要去重的话，是因为**不能进行排序**，因此需要借助Set对同一层的值进行去重
  - 本质：借助Set进行同层上的数值判断，以及子序列是否合法