# Search in Rotated Sorted Array

**Link:** https://leetcode.com/problems/search-in-rotated-sorted-array/

## Approach

**Brute force:** Linear scan through the array to find the target. O(n) time.

**Optimized:** Binary search with awareness of the rotation. At every midpoint, one half of the array is guaranteed to be sorted. Determine which half is sorted, then check if the target falls within that sorted range to decide which half to continue searching in.

**Why it works:** Even though the array is rotated, at least one of the two halves around `mid` is always sorted. By comparing `nums[mid]` with `nums[r]`, we can tell which half is sorted. If `nums[mid] > nums[r]`, the left half is sorted; otherwise the right half is sorted. We then check if the target lies in the sorted half and move accordingly.

## Code

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums) - 1

        while l <= r:
            mid = (l + r) // 2

            if nums[mid] == target:
                return mid

            if nums[mid] > nums[r]:
                if nums[l] <= target <= nums[mid]:
                    r = mid - 1
                else:
                    l = mid + 1
            else:
                if nums[mid] <= target <= nums[r]:
                    l = mid + 1
                else:
                    r = mid - 1

        return -1
```

## Complexity

Time: O(log n)  
Space: O(1)
