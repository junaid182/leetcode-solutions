# Remove Element

**Link:** https://leetcode.com/problems/remove-element/

## Approach

**Brute force:** Create a new array with only elements that don't equal `val`, copy it back into `nums`. Uses extra space.

**Optimized:** Two-pointer in-place. `k` tracks the write position (next slot for a valid element). `i` scans every element — whenever `nums[i] != val`, write it to `nums[k]` and advance `k`. Elements equal to `val` are simply skipped.

**Why it works:** `k` always points to the next available slot for a non-val element. By the end, the first `k` elements of `nums` contain all valid values in their original order, and `k` is the count.

## Code

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        k = 0

        for i in range(len(nums)):
            if nums[i] != val:
                nums[k] = nums[i]
                k += 1

        return k
```

## Complexity

Time: O(n) — single pass through the array
Space: O(1) — in-place, no extra memory used
