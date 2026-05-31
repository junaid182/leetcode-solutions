# House Robber II

**Link:** https://leetcode.com/problems/house-robber-ii/

## Approach

The circular constraint means the first and last houses are adjacent — you can't rob both. Split into two linear subproblems: `nums[:-1]` (exclude last) and `nums[1:]` (exclude first). Run House Robber on each and return the max.

The inner `robberhouse` function is the same rolling-window DP from House Robber I.

## Code

```python
class Solution:
    def rob(self, nums: List[int]) -> int:

        def houseRobber(nums_arr):

            prev2 = nums_arr[0]
            prev1 = max(nums_arr[0], nums_arr[1])

            for i in range(2, len(nums_arr)):
                cur = max(prev1, prev2 + nums_arr[i])

                prev2 = prev1
                prev1 = cur

            return prev1
        
        if len(nums) <= 2:
            return max(nums)
        
        return max(houseRobber(nums[1:]), houseRobber(nums[:-1]))
```

## Complexity

Time: O(n) — two linear passes  
Space: O(1)
