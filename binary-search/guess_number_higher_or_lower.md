# Guess Number Higher or Lower

**Link:** https://leetcode.com/problems/guess-number-higher-or-lower/

## Approach

**Brute force:** Try every number from 1 to n, calling `guess()` on each. O(n) time.

**Optimized:** Binary search over the range `[1, n]`. Use the `guess()` API result to decide which half to search:
- `-1` means our guess is too high → search left.
- `1` means our guess is too low → search right.
- `0` means correct → return mid.

**Why it works:** The search space is sorted (1 to n), so binary search is valid. Each call halves the range, guaranteeing we find the number in O(log n).

## Code

```python
class Solution:
    def guessNumber(self, n: int) -> int:
        l, r = 1, n

        while l <= r:
            mid = (l + r) // 2
            res = guess(mid)

            if res < 0:
                r = mid - 1
            elif res > 0:
                l = mid + 1
            else:
                return mid
```

## Complexity

Time: O(log n)
Space: O(1)
