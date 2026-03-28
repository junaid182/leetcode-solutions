# Contains Duplicate

**Link:** https://leetcode.com/problems/contains-duplicate/

## Approach

**Brute force:** Compare every pair of elements — O(n²) time.

**Optimized:** Use a hash set to track seen numbers. For each element, check if it's already in the set; if so, return `True`. Otherwise, add it.

**Why it works:** A set provides O(1) average-case lookup, so we can detect a duplicate in a single pass.

## Code

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        numsSet = set()

        for n in nums:
            if n in numsSet:
                return True
            numsSet.add(n)

        return False
```

## Complexity

Time: O(n)
Space: O(n)
