# Combination Sum

**Link:** https://leetcode.com/problems/combination-sum/

## Approach

DFS with two choices at each index: include `candidates[i]` again (staying at `i`) or skip to the next candidate (`i+1`). Accumulate the running total and record the combination when it hits the target.

**Why it works:** Allowing re-use by not advancing `i` on the "include" branch covers all repetitions. Advancing `i` on the "skip" branch ensures no duplicate combinations (each candidate is only reconsidered going left-to-right).

## Code

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:

        res = []

        subset = []
        def dfs(i, total):
            if total == target:
                res.append(subset.copy())
                return
            
            if total > target or i == len(candidates):
                return
            
            subset.append(candidates[i])
            dfs(i, candidates[i]+total)

            subset.pop()
            dfs(i+1, total)

        dfs(0, 0)
        return res
```

## Complexity

Time: O(2^t) — where t is target / min(candidates)  
Space: O(t) — recursion depth bounded by target
