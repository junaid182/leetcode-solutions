# Two Sum

**Link:** https://leetcode.com/problems/two-sum/

## Approach

**Brute force:** Check every pair of numbers with two nested loops. For each element, scan all elements after it to find a pair that sums to target. O(n²) time.

**Optimized:** Use a hashmap to store each number and its index as we iterate. For every number `n`, compute `second_number = target - n` and check if it already exists in the hashmap. If it does, we found our pair.

**Why it works:** Instead of looking forward (brute force), we look backward — by the time we reach the second number of a valid pair, the first number is already in the hashmap. One pass is enough.

## Code

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:

        numsHashmap = {}

        for i, n in enumerate(nums):
            second_number = target - n
            if second_number in numsHashmap:
                return numsHashmap[second_number], i
            else:
                numsHashmap[n] = i
```

## Complexity

Time: O(n) — single pass through the array
Space: O(n) — hashmap stores at most n elements
