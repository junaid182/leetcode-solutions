# Combination Sum

**Link:** https://leetcode.com/problems/combination-sum/

## Approach

Iterative start-index backtracking. At each call, iterate from `start` forward — appending the candidate, recursing with the same `i` (allowing reuse), and popping. Record the path when `total == target`, prune when it exceeds.

**Why it works:** Passing `i` (not `i+1`) on the recursive call allows a candidate to be reused. Iterating from `start` forward prevents duplicate combinations.

## Code

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []

        def backtrack(start, path, total):
            if total == target:
                res.append(path.copy())
                return
            
            if total > target:
                return
            
            for i in range(start, len(candidates)):
                path.append(candidates[i])
                backtrack(i, path, total + candidates[i])
                path.pop()

        backtrack(0, [], 0)

        return res
```

## Complexity

Time: O(2^t) — where t is target / min(candidates)  
Space: O(t) — recursion depth bounded by target
