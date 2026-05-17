# Coin Change

**Link:** https://leetcode.com/problems/coin-change/

## Approach

Bottom-up DP. Initialize `dp[0] = 0` (zero coins to make amount 0) and every other entry to `amount + 1` as a sentinel for "unreachable". For each amount `a`, try every coin — if the remainder `a - c` is valid, update `dp[a]` with the minimum coins needed.

**Why `amount + 1` as sentinel:** The maximum coins ever needed is `amount` (all 1-coins), so `amount + 1` is safely unreachable and easy to check at the end.

## Code

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [amount+1] * (amount+1)
        dp[0] = 0

        for a in range(1, amount+1):
            for c in coins:
                if a-c >= 0:
                    dp[a] = min(dp[a], 1 + dp[a-c])
        
        return dp[amount] if dp[amount] != amount+1 else -1
```

## Complexity

Time: O(amount × coins) — nested loop over amounts and coin denominations  
Space: O(amount) — dp array
