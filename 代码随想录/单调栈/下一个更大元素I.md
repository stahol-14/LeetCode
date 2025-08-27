# [下一个更大元素I](下一个更大元素I"[题目地址](https://leetcode.cn/problems/next-greater-element-i/description/)")

## 题目描述
nums1 中数字 x 的 下一个更大元素 是指 x 在 nums2 中对应位置 右侧 的 第一个 比 x 大的元素。

给你两个 没有重复元素 的数组 nums1 和 nums2 ，下标从 0 开始计数，其中nums1 是 nums2 的子集。

对于每个 0 <= i < nums1.length ，找出满足 nums1[i] == nums2[j] 的下标 j ，并且在 nums2 确定 nums2[j] 的 下一个更大元素 。如果不存在下一个更大元素，那么本次查询的答案是 -1 。

返回一个长度为 nums1.length 的数组 ans 作为答案，满足 ans[i] 是如上所述的 下一个更大元素 。

### 思路：单调栈+哈希表🌟

- 使用哈希表存放元素值作为key，比起更大的元素值作为value

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {

        // nums1是nums2的子集，在nums2中 找nums1[i]，然后看是否存在比其大的元素
        // 使用单调栈——遍历一次即可。 —— 单调栈 栈顶到栈底 递增

        // 需要通过Map处理nums2中各元素及右侧第一个更大元素的关系
        Map<Integer, Integer> map = new HashMap<>();
        Deque<Integer> stack = new ArrayDeque<>();

        for(int num : nums2){
            // 当前元素 > 栈顶元素 需要将栈内清除 并加入到map中
            while( (!stack.isEmpty()) && num > stack.peek() ){
                map.put(stack.pop(), num);
            }
            stack.push(num);
        }

        int n = nums1.length;
        int[] res = new int[n];
        for(int i = 0; i < n; i++){
            res[i] = map.getOrDefault(nums1[i], -1); // 没有找到 为-1
        }

        return res;
    }
}
```

#### 复杂度分析
时间复杂度：O(n + m)，nums1的长度为n，nums2的长度为m

空间复杂度：O(m)

### 总结
