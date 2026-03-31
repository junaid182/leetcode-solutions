# Sqrt(x)

**Link:** https://leetcode.com/problems/sqrtx/

## Approach

**Brute force:** Increment from 0 until `i*i > x`, return `i - 1`. O(sqrt(n)) time.

**Optimized:** Binary search over `[0, x]`. At each midpoint:
- If `mid²  > x`, the answer is in the left half.
- If `mid² < x`, the answer could be `mid` or higher — save `mid` as a candidate and search right.
- If `mid² == x`, exact match, return `mid`.

**Why it works:** The integer square root is the largest `mid` where `mid² <= x`. By tracking `res` whenever `mid² < x`, we always have the best valid floor value when the loop ends.

## Code

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        l, r = 1, x
        res = 0

        while l <= r:
            mid = (l + r) // 2

            sqrt = mid * mid

            if sqrt == x:
                return mid
            elif sqrt > x:
                r = mid - 1
            else:
                res = mid
                l = mid + 1

        return res
```

## Complexity

Time: O(log n)
Space: O(1)
