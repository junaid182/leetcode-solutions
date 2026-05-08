# Single Number

**Link:** https://leetcode.com/problems/single-number/

## Approach

XOR all numbers together. Every duplicate cancels out (`n ^ n = 0`), and XOR with zero is a no-op (`0 ^ n = n`). What remains is the single unique number.

## Code

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        res = 0

        for n in nums:
            res = res ^ n
        
        return res
```

## Complexity

Time: O(n) — single pass  
Space: O(1) — no extra space
