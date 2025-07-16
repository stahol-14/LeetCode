# [四数之和II](四数之和II"[题目地址](https://leetcode.cn/problems/4sum-ii/description/)")

## 题目描述
四个长度均为 `n` 的整数数组 `nums1`、`nums2`、`nums3` 和 `nums4`，计算**有多少个元组 `(i, j, k, l)` 满足**：
nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0

### 思路：哈希 + 分治思想
- 将四个数组分成两组：`(nums1 + nums2)` 和 `(nums3 + nums4)`
- 枚举 `nums1[i] + nums2[j]` 的所有组合，并用哈希表 `map` 记录每个和出现的次数；
- 枚举 `nums3[k] + nums4[l]` 的所有组合，判断 `-(c + d)` 是否在 map 中出现；
- 每当出现时，累加其频次，即为满足条件的元组数量。

```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        Map<Integer, Integer> map = new HashMap<>(); 

        for(int a : nums1){
            for(int b : nums2){
                int sum = a + b;
                map.put(sum, map.getOrDefault(sum, 0) + 1);
            }
        }

        // 判断 nums3 + nums4 对应的值 是否符合
        int count = 0;
        for(int c : nums3){
            for(int d : nums4){
                int sum = -(c + d);
                if(map.containsKey(sum)){
                    count += map.get(sum);
                }
            }
        }

        return count;
    }
}
```

#### 复杂度分析
时间复杂度：O(n²)，构建mapO(n²)，第二轮查找O(n²)
空间复杂度：O(n²)，哈希表最多存储 n² 个不同的 (a + b) 值

### 总结