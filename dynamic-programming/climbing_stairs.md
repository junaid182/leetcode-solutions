# Climbing Stairs

**Link:** https://leetcode.com/problems/climbing-stairs/

## Approach

At each step, you can arrive from either one step below or two steps below. This makes the number of ways to reach step `n` equal to `ways(n-1) + ways(n-2)` — identical to Fibonacci.

Instead of storing the full DP array, keep only the last two values (`one` and `two`). On each iteration, shift them forward: `one` becomes `one + two`, and `two` takes the old `one`. After `n-1` iterations, `one` holds the answer.

Base case: both start at `1` because there is exactly one way to reach step 0 (do nothing) and step 1 (one single step).

## Code

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        one, two = 1, 1

        for i in range(n-1):
            temp = one
            one = one + two
            two = temp
        
        return one
```

## Complexity

Time: O(n) — single loop up to n-1
Space: O(1) — only two variables maintained
