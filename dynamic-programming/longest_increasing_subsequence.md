# Longest Increasing Subsequence

**Link:** https://leetcode.com/problems/longest-increasing-subsequence/

## Approach

Bottom-up DP from right to left. `dp[i]` is the length of the longest increasing subsequence starting at index `i`. Each position looks ahead at all `j > i` — if `nums[i] < nums[j]`, then `nums[i]` can extend the subsequence at `j`, so `dp[i] = max(dp[i], 1 + dp[j])`. Every position starts at `1` (just itself).

## Code

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        dp = [1] * len(nums)

        for i in range(len(nums)-1, -1, -1):
            for j in range(i+1, len(nums)):
                if nums[i] < nums[j]:
                    dp[i] = max(dp[i], 1+dp[j])
        
        return max(dp)
```

## Complexity

Time: O(n²) — nested loop over all pairs  
Space: O(n) — dp array
