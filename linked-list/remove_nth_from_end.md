# Remove Nth Node From End of List

**Link:** https://leetcode.com/problems/remove-nth-node-from-end-of-list/

## Approach

**Brute force:** Traverse the list to get its length, then traverse again to the (length - n)th node and remove the next node. Two passes, O(n) time.

**Optimized:** Use two pointers with a gap of n between them. Advance `right` n steps ahead, then move both `left` and `right` together until `right` hits the end. At that point `left` is just before the target node.

**Why it works:** The gap of n means when `right` reaches the end, `left` is exactly n nodes behind — pointing to the predecessor of the node to remove. A dummy head node handles the edge case where the head itself is removed.

## Code

```python
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        first = dummy
        second = head

        for i in range(n):
            second = second.next

        while second:
            first = first.next
            second = second.next

        first.next = first.next.next

        return dummy.next
```

## Complexity

Time: O(n)  
Space: O(1)
