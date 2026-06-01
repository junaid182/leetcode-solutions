# Permutations

**Link:** https://leetcode.com/problems/permutations/

## Approach

Iterative backtracking with a `visited` set tracking values. At each call, try every value not yet in `visited` — mark it, append it, recurse, then remove and unmark (backtrack). Record the path when it reaches full length.

## Code

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res = []

        visited = set()
        def backtrack(path):
            if len(path) == len(nums):
                res.append(path.copy())
                return
            
            for i in range(len(nums)):
                if nums[i] in visited:
                    continue
                
                visited.add(nums[i])
                path.append(nums[i])
                backtrack(path)
                path.remove(nums[i])
                visited.remove(nums[i])

        backtrack([])

        return res
```

## Complexity

Time: O(n! · n) — n! permutations, each requiring O(n) to build  
Space: O(n! · n) — storing all permutations
