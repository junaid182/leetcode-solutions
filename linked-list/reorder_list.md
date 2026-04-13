# Reorder List

**Link:** https://leetcode.com/problems/reorder-list/

## Approach

**Brute force:** Store all nodes in an array, then use two pointers (left and right) to rebuild the list in the required order. O(n) space.

**Optimized:** Three-step in-place approach:
1. Find the middle of the list using slow/fast pointers.
2. Reverse the second half of the list.
3. Merge the two halves by alternating nodes.

**Why it works:** Splitting at the middle gives two halves of equal (or near-equal) length. Reversing the second half means its traversal order aligns with what the reordering requires — we just zip the two halves together.

## Code

```python
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        slow, fast = head, head.next

        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        second = slow.next
        slow.next = None

        prev = None
        while second:
            temp = second.next
            second.next = prev
            prev = second
            second = temp

        first, second = head, prev

        while second:
            temp1, temp2 = first.next, second.next
            first.next = second
            second.next = temp1
            first, second = temp1, temp2
```

## Complexity

Time: O(n)  
Space: O(1)
