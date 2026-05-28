# Min Cost Climbing Stairs

**Link:** https://leetcode.com/problems/min-cost-climbing-stairs/

## Approach

Seed `prev2 = cost[0]` and `prev1 = cost[1]`. Iterate forward — at each step the minimum total cost is `cost[i] + min(prev2, prev1)`. Shift the window and return the smaller of the final two values.

## Code

```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:

        prev2 = cost[0]
        prev1 = cost[1]

        for i in range(2, len(cost)):
            cur = cost[i] + min(prev2, prev1)

            prev2 = prev1
            prev1 = cur
        
        return min(prev1, prev2)
```

## Complexity

Time: O(n) — single backwards pass
Space: O(1) — modified in-place, no extra array
