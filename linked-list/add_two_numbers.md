# Add Two Numbers

**Link:** https://leetcode.com/problems/add-two-numbers/

## Approach

**Brute force:** Extract both numbers into integers, add them, then rebuild the linked list from the result. Fails for very large numbers due to integer overflow.

**Optimized:** Simulate grade-school addition digit by digit. Traverse both lists simultaneously, summing corresponding values plus any carry. Append each resulting digit to a new list built with a dummy head.

**Why it works:** The digits are already stored in reverse order, so iterating forward naturally processes least-significant digits first — exactly how addition works. The loop continues as long as either list has nodes or there is a remaining carry, handling unequal lengths and a final carry-out cleanly.

## Code

```python
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(0, None)
        cur = dummy
        carry = 0

        while l1 or l2 or carry:
            val1 = l1.val if l1 else 0
            val2 = l2.val if l2 else 0

            sum = val1 + val2 + carry

            carry = sum // 10
            remainder = sum % 10

            cur.next = ListNode(remainder, None)
            cur = cur.next

            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None

        return dummy.next
```

## Complexity

Time: O(max(m, n))  
Space: O(max(m, n))
