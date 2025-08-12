# [爬楼梯plus](爬楼梯plus"[题目地址](https://kamacoder.com/problempage.php?pid=1067)")

## 题目描述
假设你正在爬楼梯。需要 n 阶你才能到达楼顶。 

每次你可以爬至多m (1 <= m < n)个台阶。你有多少种不同的方法可以爬到楼顶呢？ 

注意：给定 n 是一个正整数。

### 思路：完全背包（dp）


```java
import java.util.Scanner;

public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(); // 要爬的台阶数
        int m = sc.nextInt(); // 每次最多可以爬的台阶数

        // 每次都可以选择爬 1-m阶 台阶，可以重复 ==> 完全背包
        // 存在 顺序 ==> 排列数 ==> 先背包 再物品
        int[] dp = new int[n + 1];
        dp[0] = 1; // 初始化，第0阶只有一种可能

        for(int i = 1; i <= n; i++){
            for(int j = 0; j <= m; j++){
                if(i >= j){
                    // 当前台阶数 大于等于 当前打算走的台阶数
                    dp[i] += dp[i - j];
                }
            }
        }

        System.out.println(dp[n]);
        sc.close();
    }
}
```

#### 复杂度分析
时间复杂度：O(n * m)

空间复杂度：O(n)

### 总结
