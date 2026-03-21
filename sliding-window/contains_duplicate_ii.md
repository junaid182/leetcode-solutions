# Contains Duplicate II

**Link:** https://leetcode.com/problems/contains-duplicate-ii/

## Approach

**Brute force:** For every element, check all previous elements within distance k to see if any match. O(n * k) time.

**Optimized:** Sliding window of size k using a set. Advance the right pointer through the array, shrink the window from the left when its size exceeds k, and check if the current element already exists in the window.

**Why it works:** The set always holds at most k elements — the last k values seen. If the current number is already in the set, there must be a duplicate within k indices. Removing `nums[L]` before sliding keeps the window exactly size k.

## Code

```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        window = set()
        L = 0

        for R in range(len(nums)):
            if R - L > k:
                window.remove(nums[L])
                L += 1

            if nums[R] in window:
                return True
            window.add(nums[R])

        return False
```

## Complexity

Time: O(n) — single pass through the array
Space: O(k) — the window set holds at most k elements
