# Linked List Cycle

**Link:** https://leetcode.com/problems/linked-list-cycle/

## Approach

**Brute force:** Store every visited node in a hash set. At each step, check if the current node is already in the set — if so, a cycle exists. O(n) time and O(n) space.

**Optimized:** Use Floyd's cycle detection (two pointers). A `slow` pointer advances one step at a time while a `fast` pointer advances two. If there's a cycle, fast will eventually lap slow and they'll meet. If there's no cycle, fast will reach the end.

**Why it works:** In a cycle, fast gains one step on slow per iteration. Since fast is always closing the gap, they must meet inside the cycle within at most `n` steps.

## Code

```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow, fast = head, head

        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

            if slow == fast:
                return True

        return False
```

## Complexity

Time: O(n) — fast pointer traverses the list at most twice
Space: O(1) — only two pointers used
