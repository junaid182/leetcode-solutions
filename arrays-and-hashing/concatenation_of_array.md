# Concatenation of Array

**Link:** https://leetcode.com/problems/concatenation-of-array/

## Approach

**Brute force:** Append all elements of `nums` twice into a new array.

**Optimized:** Same — iterate over `nums` twice using a loop, appending each element.

**Why it works:** The result array `ans` of length `2n` is just `nums` followed by itself. Iterating twice and appending each element builds exactly that.

## Code

```python
class Solution:
    def getConcatenation(self, nums: List[int]) -> List[int]:
        ans = []

        for _ in range(2):
            for n in nums:
                ans.append(n)

        return ans
```

## Complexity

Time: O(n)
Space: O(n)
