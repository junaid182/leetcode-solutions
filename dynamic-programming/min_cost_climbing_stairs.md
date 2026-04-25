# Min Cost Climbing Stairs

**Link:** https://leetcode.com/problems/min-cost-climbing-stairs/

## Approach

Work backwards through the `cost` array. Append a `0` to the end representing the top of the staircase (reaching it has no additional cost).

For each step `i`, the cheapest path forward is whichever is cheaper — taking one step or two steps. Update in-place:

```
cost[i] = cost[i] + min(cost[i+1], cost[i+2])
```

Start from the third-to-last index and move left, so `cost[i+1]` and `cost[i+2]` are already resolved when we process `i`. At the end, `cost[0]` and `cost[1]` hold the total minimum cost of reaching the top from each starting position — return the smaller of the two.

## Code

```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        cost.append(0)

        for i in range(len(cost) - 3, -1, -1):
            cost[i] = min(cost[i] + cost[i+1], cost[i] + cost[i+2])
        
        return min(cost[0], cost[1])
```

## Complexity

Time: O(n) — single backwards pass
Space: O(1) — modified in-place, no extra array
