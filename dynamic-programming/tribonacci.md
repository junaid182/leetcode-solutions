# N-th Tribonacci Number

**Link:** https://leetcode.com/problems/n-th-tribonacci-number/

## Approach

The Tribonacci sequence extends Fibonacci by summing the previous three values instead of two: `T(n) = T(n-1) + T(n-2) + T(n-3)`, with base cases `T(0)=0`, `T(1)=1`, `T(2)=1`.

Keep a rolling window of three values. On each iteration, shift left and set the new tail to the sum of all three. Tuple unpacking evaluates the right-hand side before assigning, so no temporary variable is needed.

## Code

```python
class Solution:
    def tribonacci(self, n: int) -> int:
        t = [0, 1, 1]

        if n < 3:
            return t[n]

        for i in range(3, n+1):
            t[0], t[1], t[2] = t[1], t[2], sum(t)
        
        return t[2]
```

## Complexity

Time: O(n) — single loop up to n
Space: O(1) — only three variables maintained
