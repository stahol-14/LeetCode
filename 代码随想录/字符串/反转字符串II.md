# [反转字符串II](反转字符串II"[题目地址](https://leetcode.cn/problems/reverse-string-ii/)")

## 题目描述
给定一个字符串 `s` 和一个整数 `k`，从字符串开头开始，按照下述规则处理每个 2k 字符：

- 如果剩余字符少于 `k` 个，则将**剩余字符全部反转**；
- 如果剩余字符大于等于 `k` 但小于 `2k`，则只**反转前 `k` 个字符**；
- 如果剩余字符大于等于 `2k`，每次取 `2k` 个字符，其中**前 `k` 个字符反转，其余保留原样**。

### 思路：原地反转 + 双指针


```java
class Solution {
    public String reverseStr(String s, int k) {
        char[] ch = s.toCharArray(); // 将字符串转为字符数组
        int n = ch.length;

        // 每隔 2k 个字符，反转前 k 个字符
        for (int i = 0; i < n; i += 2 * k) {
            int end = Math.min(i + k - 1, n - 1); // 控制反转范围，避免越界
            reverse(ch, i, end); // 反转 ch[i..end]
        }

        return new String(ch); // 返回最终字符串
    }

    // 原地反转字符数组中 ch[start..end] 区间的字符
    private void reverse(char[] ch, int start, int end) {
        while (start < end) {
            char temp = ch[start];
            ch[start] = ch[end];
            ch[end] = temp;
            start++;
            end--;
        }
    }
}
```

#### 复杂度分析
时间复杂度：O(n)
空间复杂度：O(n) — 字符数组复制（原地在 char[] 上反转）

### 总结