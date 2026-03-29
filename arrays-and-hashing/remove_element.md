# Remove Element

**Link:** https://leetcode.com/problems/remove-element/

## Approach

**Brute force:** Create a new list filtering out the target value, then copy it back. Uses extra space.

**Optimized:** Use a write pointer `k` that tracks the next valid position. Iterate through the array — when a value doesn't match `val`, write it at position `k` and advance `k`. In-place with no extra memory.

**Why it works:** Elements not equal to `val` are compacted to the front. The first `k` elements hold the valid values, and `k` is the count of non-`val` elements.

## Code

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        k = 0

        for n in nums:
            if n != val:
                nums[k] = n
                k += 1

        return k
```

## Complexity

Time: O(n)
Space: O(1)
