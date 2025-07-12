# [删除链表的倒数第N个节点](删除链表的倒数第N个节点"题目地址")

## 题目描述
给你一个链表，删除链表的倒数第 `n` 个结点，并返回链表的头结点。
### 思路：快慢指针
- 使用两个指针 `fast` 和 `slow`。
- `fast` 先比 `slow` 多走 `n` 步。
- 然后 `fast` 和 `slow` 同时向前移动，直到 `fast` 到达链表末尾。
- 此时 `slow.next` 就是要被删除的节点。

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummyHead = new ListNode(0, head);
        ListNode fast = dummyHead, slow = dummyHead;

        // fast 先向前移动 n 步
        for (int i = 0; i < n; i++) {
            fast = fast.next;
        }

        // fast 和 slow 一起移动，直到 fast 到达链表尾部
        // 此时 slow 的下一个节点是要被删除的节点
        while (fast.next != null) {
            fast = fast.next;
            slow = slow.next;
        }

        // 删除 slow 的下一个节点
        slow.next = slow.next.next;

        // 返回头节点（即 dummyHead.next）
        return dummyHead.next;
    }
}
```

#### 复杂度分析
时间复杂度：O(n)
空间复杂度：O(1)

### 总结