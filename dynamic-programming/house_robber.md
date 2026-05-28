# House Robber

**Link:** https://leetcode.com/problems/house-robber/

## Approach

Seed `prev2 = nums[0]` and `prev1 = max(nums[0], nums[1])` — the best loot from the first one or two houses. For each subsequent house, take the better of robbing it (`prev2 + nums[i]`) or skipping it (`prev1`). Shift the window forward.

## Code

```python
class Solution:
    def rob(self, nums: List[int]) -> int:

        if len(nums) == 1:
            return nums[0]

        prev2 = nums[0]
        prev1 = max(nums[0], nums[1])

        for i in range(2, len(nums)):
            cur = max(prev2+nums[i], prev1)

            prev2 = prev1
            prev1 = cur
        
        return max(prev1, prev2)
```

## Complexity

Time: O(n) — single pass  
Space: O(1) — two variables only
