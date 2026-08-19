# Happy Number

**Link:** https://leetcode.com/problems/happy-number/

## Approach

**Brute force:** Repeatedly replace `n` with the sum of squares of its digits. If any cycle is detected (via a visited set), it's not happy. If it reaches 1, it is.

**Optimized:** Same approach — use a visited set to detect cycles. Extract a `sumOfSquares` helper to keep the main loop clean.

**Why it works:** For any non-happy number, the sequence of sums will eventually enter a cycle that never reaches 1. Tracking seen values lets us detect the cycle in O(log n) space (bounded by the number of distinct sums, which is small).

## Code

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        visit = set()

        while True:
            n = self.sumOfSquares(n)

            if n in visit:
                return False

            if n == 1:
                return True
            else:
                visit.add(n)
                
        
        return False
    
    def sumOfSquares(self, n):
        res = 0

        while n:
            mod = n % 10
            n = n // 10
            res += mod ** 2
        
        return res
```

## Complexity

Time: O(log n) — number of digits processed per iteration; bounded cycle length  
Space: O(log n) — visited set size is bounded
