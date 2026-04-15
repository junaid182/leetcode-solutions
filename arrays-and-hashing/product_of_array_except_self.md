# Product of Array Except Self

**Link:** https://leetcode.com/problems/product-of-array-except-self/

## Approach

**Brute force:** For each element, multiply all other elements — O(n²) time.

**Optimized:** Use prefix and postfix products. For each index `i`, the result is the product of all elements to the left (prefix) multiplied by the product of all elements to the right (postfix). Do two passes: left-to-right to fill prefix products, right-to-left to multiply in postfix products — all stored in the output array itself.

**Why it works:** Every element in the result needs the product of everything except itself. Splitting into prefix × postfix lets us compute this in O(n) without division and without extra space (beyond the output array).

## Code

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        res = []
        prefix = 1
        for n in nums:
            res.append(prefix)
            prefix = prefix * n

        postfix = 1
        for i in range(len(res) - 1, -1, -1):
            res[i] = res[i] * postfix
            postfix = postfix * nums[i]

        return res
```

## Complexity

Time: O(n)  
Space: O(1) — output array excluded
