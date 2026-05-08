# Number of 1 Bits

**Link:** https://leetcode.com/problems/number-of-1-bits/

## Approach

Use the trick `n & (n - 1)` to clear the lowest set bit of `n` on each iteration. Count how many times this can be done before `n` reaches zero — that count is the number of `1` bits.

**Why it works:** Subtracting 1 flips the lowest set bit to `0` and all bits below it to `1`. ANDing with `n` clears all of those, leaving only the bits above the lowest set bit unchanged. Each iteration removes exactly one `1` bit.

## Code

```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        res = 0

        while n:
            n = n & (n - 1)
            res += 1
        
        return res
```

## Complexity

Time: O(k) — where k is the number of set bits (at most 32)  
Space: O(1)
