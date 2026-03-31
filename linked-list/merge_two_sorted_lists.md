# Merge Two Sorted Lists

**Link:** https://leetcode.com/problems/merge-two-sorted-lists/

## Approach

**Brute force:** Collect all values from both lists into an array, sort it, then build a new linked list. O(n log n) time and O(n) space.

**Optimized:** Use a dummy node as the head of the result list and a `tail` pointer to build it incrementally. At each step, compare the current nodes of both lists and attach the smaller one to `tail`, then advance that list's pointer. Once either list is exhausted, append the remainder of the other directly.

**Why it works:** Both lists are already sorted, so a single greedy comparison at each step always picks the next smallest node. The dummy node eliminates the edge case of initializing the head separately.

## Code

```python
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        tail = dummy

        while list1 and list2:
            if list1.val <= list2.val:
                tail.next = list1
                list1 = list1.next
            else:
                tail.next = list2
                list2 = list2.next
            tail = tail.next

        if list1:
            tail.next = list1
        if list2:
            tail.next = list2

        return dummy.next
```

## Complexity

Time: O(n + m) — each node from both lists is visited once
Space: O(1) — nodes are reused, only pointers are changed
