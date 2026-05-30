# Permutations

**Link:** https://leetcode.com/problems/permutations/

## Approach

Iterative backtracking with a `used` set tracking indices. At each call, try every index not yet in `used` — mark it, append the value, recurse, then pop and unmark (backtrack). Record the path when it reaches full length.

**Why track indices instead of values:** Tracking `i` (not `nums[i]`) works correctly even if duplicate values exist in the input.

## Code

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res = []

        used = set()

        def backtrack(path):
            if len(path) == len(nums):
                res.append(path.copy())
                return
            
            for i in range(len(nums)):
                if i in used:
                    continue

                used.add(i)
                path.append(nums[i])
                backtrack(path)
                path.pop()
                used.remove(i)

        backtrack([])

        return res
```

## Complexity

Time: O(n! · n) — n! permutations, each requiring O(n) to build  
Space: O(n! · n) — storing all permutations
