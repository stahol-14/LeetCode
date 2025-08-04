# [K次取反后最大化的数组和](K次取反后最大化的数组和"[题目地址](https://leetcode.cn/problems/maximize-sum-of-array-after-k-negations/description/)")

## 题目描述
给你一个整数数组 nums 和一个整数 k ，按以下方法修改该数组：

- 选择某个下标 i 并将 nums[i] 替换为 -nums[i] 。
- 重复这个过程恰好 k 次。可以多次选择同一个下标 i 。

以这种方式修改数组后，返回数组 可能的最大和 。

### 思路：贪心
- 优先将数组中 负数变为正数
- 如果全为正数了，那么需要看k是否用完
  - 如果k为偶数，不需要变
  - 如果k为奇数，只需要对最小值取反


```java
class Solution {
    public int largestSumAfterKNegations(int[] nums, int k) {
        // 要得到最大的数组和，取反需要 找最小值取反（负数变大，正数变小的最少）
        Arrays.sort(nums); // 排序——方便找最小

        int i = 0;
        // 1. 把尽可能多的负数变成正数
        while(k > 0 && i < nums.length && nums[i] < 0){
            nums[i] = -nums[i];
            i++;
            k--;
        } 

        // 2. 如果还有k 则只取反最小值一次
        if(k % 2 == 1){ 
            Arrays.sort(nums);
            nums[0] = -nums[0];
        }

        // 3. 求最终和
        int sum = 0;
        for(int num : nums){
            sum += num;
        }
        
        return sum;
    }
}
```

#### 复杂度分析
时间复杂度：O(nlogn)——排序的时间复杂度
空间复杂度：O(1)

### 总结
