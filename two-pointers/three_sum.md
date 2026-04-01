# 3Sum

**Link:** https://leetcode.com/problems/3sum/

## Approach

**Brute force:** Check every triplet with three nested loops. O(n³) time.

**Optimized:** Sort the array, then for each element use two pointers on the remaining subarray to find pairs that sum to its negative. Skip duplicates at both the outer loop and after finding a valid triplet to avoid duplicate results.

**Why it works:** Sorting lets two pointers work correctly (move left up to increase sum, move right down to decrease). Skipping duplicates at `i` ensures we don't process the same first element twice; skipping duplicates at `l` after a match ensures we don't emit the same triplet twice.

## Code

```python
class Solution:
    def threeSum(self, nums: list[int]) -> list[list[int]]:
        res = []
        nums.sort()

        for i, a in enumerate(nums):
            if i > 0 and nums[i] == nums[i - 1]:
                continue

            l, r = i + 1, len(nums) - 1

            while l < r:
                threeSum = a + nums[l] + nums[r]

                if threeSum == 0:
                    res.append([a, nums[l], nums[r]])
                    l += 1

                    while l < r and nums[l] == nums[l - 1]:
                        l += 1
                elif threeSum > 0:
                    r = r - 1
                else:
                    l = l + 1

        return res
```

## Complexity

Time: O(n²) — O(n log n) sort + O(n²) for the outer loop with two pointers
Space: O(1) — excluding the output list
