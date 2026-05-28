# Decode Ways

**Link:** https://leetcode.com/problems/decode-ways/

## Approach

Backward DP with two rolling variables. `next1 = dp[i+1]` (ways from one step ahead) and `next2 = dp[i+2]` (ways from two steps ahead). Base case: `next1 = 1` (empty suffix has one decoding), `next2 = 0`.

For each position `i`:
- If `s[i] != '0'`: single-digit decode is valid → `cur += next1`
- If `s[i:i+2]` forms a valid two-digit number (10–26): `cur += next2`
- Shift: `next2 = next1`, `next1 = cur`

## Code

```python
class Solution:
    def numDecodings(self, s: str) -> int:
        n = len(s)

        next1 = 1 # dp[n]
        next2 = 0 # dp[n+1]

        for i in range(n-1, -1, -1):
            cur = 0

            if s[i] != "0":
                cur = next1

                if i+1 < n and (s[i] == "1" or (s[i] == "2" and s[i+1] in "0123456")):
                    cur += next2
                
            next2 = next1
            next1 = cur
        
        return next1
```

## Complexity

Time: O(n) — single backward pass  
Space: O(1) — two variables
