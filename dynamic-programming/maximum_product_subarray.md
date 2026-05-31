# Maximum Product Subarray

**Link:** https://leetcode.com/problems/maximum-product-subarray/

## Approach

Track both `curMax` and `curMin` at each position — a negative number can flip the minimum into the maximum. For each element, compute the new max and min from three candidates: `n * curMax`, `n * curMin`, and `n` alone (starting fresh). Reset both to `1` on a zero since any subarray through zero has product zero.

`tempCurMax` preserves the old `curMax` before it's overwritten, since `curMin` needs it.

## Code

```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        res = max(nums)
        maxCur, minCur = 1, 1

        for n in nums:
            if n == 0:
                maxCur, minCur = 1, 1
            
            tempMaxCur = n * maxCur
            maxCur = max(n * maxCur, n * minCur, n)
            minCur = min(tempMaxCur, n * minCur, n)

            res = max(res, maxCur)
        
        return res
```

## Complexity

Time: O(n) — single pass  
Space: O(1)
