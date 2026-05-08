# Counting Bits

**Link:** https://leetcode.com/problems/counting-bits/

## Approach

Every number `i` can be expressed as `offset + (i - offset)`, where `offset` is the largest power of 2 ≤ `i`. The leading bit contributes `1`, and the remainder `(i - offset)` is a smaller number whose bit count is already computed.

Track `offset` as you iterate: when `offset * 2 == i`, advance `offset` to `i` (the next power of 2). Then `dp[i] = 1 + dp[i - offset]` builds the answer in one pass.

## Code

```python
class Solution:
    def countBits(self, n: int) -> List[int]:
        res = [0] * (n + 1)
        offset = 1

        for i in range(1, n+1):
            if offset * 2 == i:
                offset = i
            res[i] = 1 + res[i-offset]
        
        return res
```

## Complexity

Time: O(n) — single pass from 1 to n  
Space: O(n) — output array only, no extra space
