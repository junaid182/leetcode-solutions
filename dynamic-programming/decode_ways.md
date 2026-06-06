# Decode Ways

**Link:** https://leetcode.com/problems/decode-ways/

## Approach

Forward DP where `dp[i]` = number of ways to decode `s[:i]`. Base case: `dp[0] = 1` (empty prefix has one decoding).

For each position `i`:
- Single-char decode: if `s[i-1] != '0'` → `dp[i] += dp[i-1]`
- Two-char decode: if `s[i-2:i]` forms a valid number (10–19, or 20–26) → `dp[i] += dp[i-2]`

## Code

```python
class Solution:
    def numDecodings(self, s: str) -> int:
        n = len(s)
        dp = [0] * (n+1)
        dp[0] = 1

        for i in range(1, n+1):
            
            if s[i-1] != "0":
                dp[i] += dp[i-1]

            if i>=2 and (s[i-2] == "1" or (s[i-2] == "2" and s[i-1] in "0123456")):
                dp[i] += dp[i-2]
        
        return dp[n]
```

## Complexity

Time: O(n) — single forward pass  
Space: O(n) — dp array
