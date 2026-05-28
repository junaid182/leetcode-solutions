# Climbing Stairs

**Link:** https://leetcode.com/problems/climbing-stairs/

## Approach

At each step, you can arrive from either one step below or two steps below. This makes the number of ways to reach step `n` equal to `ways(n-1) + ways(n-2)` — identical to Fibonacci.

Keep two variables: `prev1 = 1` (ways for n=1) and `prev2 = 2` (ways for n=2). Iterate forward from 3 to n, computing `cur = prev1 + prev2` and shifting the window. Return `prev2`.

## Code

```python
class Solution:
    def climbStairs(self, n: int) -> int:

        if n < 2:
            return n
        
        prev1 = 1
        prev2 = 2

        for i in range(3, n+1):
            cur = prev1 + prev2
            prev1 = prev2
            prev2 = cur
        return prev2
```

## Complexity

Time: O(n) — single loop up to n-1
Space: O(1) — only two variables maintained
