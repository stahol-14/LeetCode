# [下一个更大元素II](下一个更大元素II"[题目地址](https://leetcode.cn/problems/next-greater-element-ii/description/)")

## 题目描述
给定一个循环数组 nums （ nums[nums.length - 1] 的下一个元素是 nums[0] ），返回 nums 中每个元素的 下一个更大元素 。

数字 x 的 下一个更大的元素 是按数组遍历顺序，这个数字之后的第一个比它更大的数，这意味着你应该循环地搜索它的下一个更大的数。如果不存在，则输出 -1 。


### 思路：单调栈+循环两遍数组


```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int n = nums.length;
        int[] res = new int[n];
        Arrays.fill(res, -1); // 默认赋值为 -1

        Deque<Integer> stack = new ArrayDeque<>();

        // 循环数组找右边第一个更大元素 —— 遍历两边即可
        for(int i = 0; i < 2 * n; i++){
            int curIndex = i % n; //  当前数组下标
            int curVal = nums[curIndex];

            while( (!stack.isEmpty()) && curVal > nums[stack.peek()] ){
                res[stack.peek()] = curVal;
                stack.pop();
            }

            if(i < n){ // 只有在第一轮遍历时 才入栈
                stack.push(curIndex);
            }
        }

        return res;
    }
}
```

#### 复杂度分析
时间复杂度：O(n)

空间复杂度：O(n)

### 总结
注：为什么选择ArrayDeque而不是Stack？
- Stack类继承自Vector，并且实现了一个标准的后进先出（LIFO）的栈。Stack的底层逻辑主要依赖于Vector
- ArrayDeque实现了Deque接口，可以用作栈（LIFO）和队列（FIFO）。它的底层实现是一个循环数组

stack和ArrayDeque的区别：

- 「stack - 线程安全 」 「ArrayDeque - 不是线程安全」
- 「stack使用动态数组」 「ArrayDeque使用循环数组」
- 由于stack为线程安全，stack的每个方法都需要获取和释放锁，额外的同步开销，从而影响性能。
- 而ArrayDeque由于没有同步开销，从而在插入和删除操作上非常高效。