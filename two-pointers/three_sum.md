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

        for a in range(len(nums) - 1):
            if a > 0 and nums[a] == nums[a - 1]:
                continue

            b, c = a + 1, len(nums) - 1

            while b < c:
                sum = nums[a] + nums[b] + nums[c]

                if sum == 0:
                    res.append([nums[a], nums[b], nums[c]])
                    b += 1
                    c -= 1

                    while b < c and nums[b] == nums[b - 1]:
                        b += 1
                    while b < c and nums[c] == nums[c + 1]:
                        c -= 1
                elif sum < 0:
                    b += 1
                else:
                    c -= 1

        return res
```

## Complexity

Time: O(n²) — O(n log n) sort + O(n²) for the outer loop with two pointers
Space: O(1) — excluding the output list
