# Min Cost Climbing Stairs

**Link:** https://leetcode.com/problems/min-cost-climbing-stairs/

## Approach

Work backwards through the `cost` array. For each step `i`, the cheapest path forward is whichever is cheaper — taking one step or two steps. Update in-place:

```
cost[i] = min(cost[i] + cost[i+1], cost[i] + cost[i+2])
```

Start from the third-to-last index and move left, so `cost[i+1]` and `cost[i+2]` are already resolved when we process `i`. The last two elements are never updated — they already represent the cost of stepping to the top from those positions. At the end, return the smaller of `cost[0]` and `cost[1]`.

## Code

```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:

        for i in range(len(cost)-3, -1, -1):
            cost[i] = min(cost[i] + cost[i+1], cost[i] + cost[i+2])

        return min(cost[0], cost[1])
```

## Complexity

Time: O(n) — single backwards pass
Space: O(1) — modified in-place, no extra array
