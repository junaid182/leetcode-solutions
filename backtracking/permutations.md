# Permutations

**Link:** https://leetcode.com/problems/permutations/

## Approach

Recursive insertion: get all permutations of `nums[1:]`, then insert `nums[0]` at every possible position in each of those permutations.

Base case: an empty list has one permutation — the empty list itself.

**Why it works:** Every permutation of n elements can be formed by taking a permutation of n-1 elements and inserting the new element at one of the n available positions. This covers all n! arrangements without duplicates.

## Code

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:

        if len(nums) == 0:
            return [[]]
        
        perms = self.permute(nums[1:])

        res = []
        for p in perms:
            for i in range(len(p) + 1):
                p_copy = p.copy()
                p_copy.insert(i, nums[0])
                res.append(p_copy)
        
        return res
```

## Complexity

Time: O(n! · n) — n! permutations, each requiring O(n) to build  
Space: O(n! · n) — storing all permutations
