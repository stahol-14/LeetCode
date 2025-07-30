# [复原IP地址](复原IP地址"[题目地址](https://leetcode.cn/problems/restore-ip-addresses/description/)")

## 题目描述
有效 IP 地址 正好由四个整数（每个整数位于 0 到 255 之间组成，且不能含有前导 0），整数之间用 '.' 分隔。

- 例如："0.1.2.201" 和 "192.168.1.1" 是 有效 IP 地址，但是 "0.011.255.245"、"192.168.1.312" 和 "192.168@1.1" 是 无效 IP 地址。

给定一个只包含数字的字符串 s ，用以表示一个 IP 地址，返回所有可能的有效 IP 地址，这些地址可以通过在 s 中插入 '.' 来形成。你 不能 重新排序或删除 s 中的任何数字。你可以按 任何 顺序返回答案。

### 思路：回溯🌟
- 分割字符串，判断是否分为了4段（每段1-3个字符），且每段是否合法

```java
class Solution {

    List<String> result = new ArrayList<>();

    public List<String> restoreIpAddresses(String s) {
        if (s.length() < 4 || s.length() > 12) return result;
        StringBuilder ip = new StringBuilder(s);
        backtracking(ip, 0, 0);
        return result;
    }

    private void backtracking(StringBuilder s, int start, int count){
        if (count == 3) {
            // 最后一个段剩余部分是否合法
            if (isValid(s, start, s.length() - 1)) {
                result.add(s.toString());
            }
            return;
        }

        for(int i = start; i < s.length(); i++){
            if (!isValid(s, start, i)) break; // 不合法直接跳出循环

            s.insert(i + 1, '.');
            backtracking(s, i + 2, count + 1); // i + 2 是下一个段起点（跳过刚插入的 '.'）
            s.deleteCharAt(i + 1); // 回溯，移除插入的 '.'
        }
    }

    private boolean isValid(StringBuilder ip, int start, int end){
        if(start > end) return false;

        // 存在前导0
        if(ip.charAt(start) == '0' && start != end) return false;

        int sum = 0;
        for(int i = start; i <= end; i++){
            int digit = ip.charAt(i) - '0';
            if (digit < 0 || digit > 9) return false;
            sum = sum * 10 + digit;
            if (sum > 255) return false;
        }
        return true;
    }
}
```

#### 复杂度分析
时间复杂度：
空间复杂度：

### 总结
