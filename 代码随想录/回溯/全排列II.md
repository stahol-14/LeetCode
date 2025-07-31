# [全排列II](全排列II"[题目地址](https://leetcode.cn/problems/permutations-ii/description/)")

## 题目描述
给定一个可包含重复数字的序列 nums ，按任意顺序 返回所有不重复的全排列。


### 思路

- 区别：可包含重复数字的序列 nums
- 直接计算得到的全排列可能重复，因此需要去重——排序

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
1. 