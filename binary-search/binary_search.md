# Binary Search

**Link:** https://leetcode.com/problems/binary-search/

## Approach

**Brute force:** Linear scan through the array — O(n).

**Optimized:** Maintain two pointers `l` and `r`. At each step, check the midpoint. If the target matches, return it. If target is smaller, discard the right half; if larger, discard the left half.

**Why it works:** The array is sorted, so comparing against the midpoint lets us eliminate half the search space each iteration, giving O(log n).

## Code

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums) - 1

        while l <= r:
            mid = (l + r) // 2

            if target == nums[mid]:
                return mid
            elif target < nums[mid]:
                r = mid - 1
            else:
                l = mid + 1

        return -1
```

## Complexity

Time: O(log n)
Space: O(1)
