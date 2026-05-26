# Permutations

**Link:** https://leetcode.com/problems/permutations/

## Approach

Iterative backtracking with a `used` set. At each call, try every number not yet in `used` — append it, mark it used, recurse, then pop and unmark (backtrack). Record the path when it reaches full length.

**Why it works:** The `used` set prevents reusing the same element in one permutation. Trying all unused elements at every position generates all n! arrangements.

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
                if nums[i] in used:
                    continue
                
                path.append(nums[i])
                used.add(nums[i])

                backtrack(path)

                path.pop()
                used.remove(nums[i])

        backtrack([])

        return res
```

## Complexity

Time: O(n! · n) — n! permutations, each requiring O(n) to build  
Space: O(n! · n) — storing all permutations
