# House Robber

**Link:** https://leetcode.com/problems/house-robber/

## Approach

Rolling DP with two variables: `rob1` (max loot up to two houses ago) and `rob2` (max loot up to the previous house). For each house, the best choice is either rob it (`rob1 + n`) or skip it (`rob2`). Shift the window forward each iteration.

```
[rob1, rob2, n, ...]
```

## Code

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        rob1, rob2 = 0, 0

        for n in nums:
            temp = max(rob1 + n, rob2)
            rob1 = rob2
            rob2 = temp
        
        return rob2
```

## Complexity

Time: O(n) — single pass  
Space: O(1) — two variables only
