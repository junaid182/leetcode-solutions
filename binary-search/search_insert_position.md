# Search Insert Position

**Link:** https://leetcode.com/problems/search-insert-position/

## Approach

**Brute force:** Linear scan through the array, return index where `nums[i] >= target`. O(n) time.

**Optimized:** Binary search. Maintain two pointers `l` and `r`. At each step, check the midpoint:
- If `nums[mid] == target`, return `mid`.
- If `target < nums[mid]`, search left half.
- If `target > nums[mid]`, search right half.

**Why it works:** After the loop, `l` points to the first index where `nums[l] >= target` — which is exactly where the target would be inserted to keep the array sorted.

## Code

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums) - 1

        while l <= r:
            mid = (l + r) // 2

            if target == nums[mid]:
                return mid
            elif target < nums[mid]:
                r = mid - 1
            else:
                l = mid + 1

        return l
```

## Complexity

Time: O(log n)
Space: O(1)
