# Search Insert Position

**Link:** https://leetcode.com/problems/search-insert-position/

## Approach

**Brute force:** Linear scan through the array and return the index where target is found or where it should be inserted. O(n) time.

**Optimized:** Binary search. Narrow the search range by comparing target to the midpoint. If target is not found, the left pointer ends up at the correct insertion index.

**Why it works:** After the loop, `l` is always the first index where `nums[l] >= target`, which is exactly where the target would be inserted to maintain sorted order.

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
