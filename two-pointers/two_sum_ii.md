# Two Sum II - Input Array Is Sorted

**Link:** https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/

## Approach

**Brute force:** Check every pair of numbers. O(n²) time.

**Optimized:** Two pointers from both ends. Since the array is sorted, if the sum is too large shrink from the right, if too small grow from the left.

**Why it works:** Sorted order guarantees that moving the left pointer up increases the sum and moving the right pointer down decreases it. We're guaranteed exactly one solution, so we'll always find it.

## Code

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l, r = 0, len(numbers) - 1

        while l < r:
            sum = numbers[l] + numbers[r]
            if sum == target:
                return [l + 1, r + 1]
            elif sum > target:
                r = r - 1
            else:
                l = l + 1
```

## Complexity

Time: O(n) — single pass with two pointers
Space: O(1) — no extra space used
