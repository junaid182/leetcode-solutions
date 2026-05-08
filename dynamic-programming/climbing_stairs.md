# Climbing Stairs

**Link:** https://leetcode.com/problems/climbing-stairs/

## Approach

At each step, you can arrive from either one step below or two steps below. This makes the number of ways to reach step `n` equal to `ways(n-1) + ways(n-2)` — identical to Fibonacci.

Instead of storing the full DP array, keep only the last two values (`one` and `two`), seeded at `2` and `1` (the answers for steps 2 and 1). Iterate backwards from `n-2` down to `1`, accumulating forward: `one` becomes `one + two`, and `two` takes the old `one`. After the loop, `one` holds the answer.

## Code

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        one, two = 2, 1

        if n < 2:
            return n

        for i in range(n-2, 0, -1):
            temp = one
            one = one + two
            two = temp
        
        return one
```

## Complexity

Time: O(n) — single loop up to n-1
Space: O(1) — only two variables maintained
