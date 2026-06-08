# Longest Increasing Subsequence

**Link:** https://leetcode.com/problems/longest-increasing-subsequence/

## Approach

Bottom-up DP from left to right. `dp[i]` is the length of the longest increasing subsequence ending at index `i`. For each `i`, look back at all `j < i` — if `nums[i] > nums[j]`, then `nums[i]` can extend the subsequence ending at `j`, so `dp[i] = max(dp[i], 1 + dp[j])`. Every position starts at `1` (just itself).

## Code

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        dp = [1] * (len(nums)+1)

        for i in range(1, len(nums)):
            for j in range(i):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i], 1 + dp[j])
        
        return max(dp)
```

## Complexity

Time: O(n²) — nested loop over all pairs  
Space: O(n) — dp array
