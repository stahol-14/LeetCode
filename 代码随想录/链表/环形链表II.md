# [环形链表II](环形链表II"[题目地址](https://leetcode.cn/problems/linked-list-cycle-ii/description/)")

## 题目描述
给定一个链表的头节点 head ，返回链表开始入环的**第一个节点**。
如果链表无环，则返回 null。

### 思路：快慢指针
> 数学推理：如果存在环，快指针每次移动2，慢指针每次移动1，则必定会在环中相遇（操场跑圈）
> 假设，入环前的距离为x，入环节点到相遇节点距离为y，相遇节点沿环到入口的距离为z，则：
> 2 * (x + y) = x + n * (y + z) + y
> x = (n - 1) * (y + z) + y, (n >= 1)
> 则：当n=1时，x = y
> 即找到相遇点后，从相遇点和头节点同时出发，会在入环的第一个节点相遇

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode fast = head, slow = head;

        // 第一步：判断链表中是否存在环（快慢指针）
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;

            // 相遇了，说明存在环
            if (fast == slow) {
                // 第二步：寻找环的起始节点
                slow = head;
                while (slow != fast) {
                    slow = slow.next;
                    fast = fast.next;
                }
                return slow; // 返回入环点
            }
        }

        // 无环
        return null;
    }
}

```

#### 复杂度分析
时间复杂度：O(n)
空间复杂度：O(1)

### 总结