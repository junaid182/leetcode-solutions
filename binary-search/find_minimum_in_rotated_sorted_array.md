# Find Minimum in Rotated Sorted Array

**Link:** https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/

## Approach

**Brute force:** Linear scan to find the minimum — O(n).

**Optimized:** Binary search. Track the current minimum. If the midpoint value is greater than the rightmost value, the minimum must be in the right half (the left half is the sorted, larger portion). Otherwise, the minimum is in the left half (including mid).

**Why it works:** In a rotated sorted array, exactly one half is always sorted. If `nums[mid] > nums[r]`, the left half is sorted and the rotation point (minimum) is to the right. Otherwise the right half is sorted and the minimum is at or to the left of mid.

## Code

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        l, r = 0, len(nums) - 1
        res = nums[0]

        while l <= r:
            mid = (l + r) // 2
            res = min(res, nums[mid])

            if nums[mid] > nums[r]:
                l = mid + 1
            else:
                r = mid - 1

        return res
```

## Complexity

Time: O(log n)
Space: O(1)
