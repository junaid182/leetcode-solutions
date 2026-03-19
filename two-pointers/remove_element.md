# Remove Element

**Link:** https://leetcode.com/problems/remove-element/

## Approach

**Brute force:** Create a new array with only elements that don't equal `val`, copy it back into `nums`. Uses extra space.

**Optimized:** Two pointers — `l` starts at the left, `r` starts at the right. When `nums[l] == val`, swap it with `nums[r]` and shrink `r` inward (that element is now "removed"). When `nums[l] != val`, advance `l`. Stop when `l > r`.

**Why it works:** Elements equal to `val` get swapped to the back of the array where they are excluded from the result. `l` ends up as the count of valid elements. Order is not preserved, but the problem doesn't require it.

## Code

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        l, r = 0, len(nums) - 1

        while l <= r:
            if nums[l] == val:
                nums[l] = nums[r]
                r -= 1
            else:
                l += 1

        return l
```

## Complexity

Time: O(n) — each element is visited at most once
Space: O(1) — in-place, no extra memory used
