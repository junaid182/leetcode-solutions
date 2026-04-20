# Subsets

**Link:** https://leetcode.com/problems/subsets/

## Approach

**Backtracking (DFS):** At each index, branch into two choices — include the element or skip it. When all elements are exhausted, record the current subset.

**Why it works:** Every subset is visited exactly once via the include/skip binary decision tree. Each leaf corresponds to a unique subset of `nums`.

## Code

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = []
        subset = []

        def dfs(i):
            if i == len(nums):
                res.append(subset.copy())
                return

            subset.append(nums[i])
            dfs(i + 1)

            subset.pop()
            dfs(i + 1)

        dfs(0)
        return res
```

## Complexity

Time: O(n · 2^n) — 2^n subsets, each copied in O(n)  
Space: O(n) — recursion stack depth
