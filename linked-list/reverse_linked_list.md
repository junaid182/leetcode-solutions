# Reverse Linked List

**Link:** https://leetcode.com/problems/reverse-linked-list/

## Approach

**Brute force:** Collect all node values into an array, reverse it, then rebuild the list. O(n) time and O(n) space.

**Optimized:** Iterative in-place reversal using two pointers (`prev` and `cur`). At each step, save the next node, reverse the current node's pointer to point at `prev`, then advance both pointers forward.

**Why it works:** By tracking `prev` and temporarily saving `cur.next`, we can redirect each node's pointer without losing the rest of the list. After the loop, `prev` sits at the new head.

## Code

```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        cur = head
        prev = None

        while cur:
            temp = cur.next
            cur.next = prev
            prev = cur
            cur = temp

        return prev
```

## Complexity

Time: O(n) — single pass through the list
Space: O(1) — only two pointers used
