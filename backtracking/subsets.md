# Subsets

**Link:** https://leetcode.com/problems/subsets/

## Approach

Record the current `path` at every recursive call (not just at leaves), then iterate from `start` forward — appending each element, recursing, and popping. Advancing `start` to `i+1` ensures each element is only considered once per path and no duplicates are generated.

**Why `path.copy()`:** Appending `path` directly would store a reference — all entries in `res` would reflect the same list as it mutates.

**vs. binary include/exclude:** This iterative-style recursion is more natural when working with combinations or subsets with constraints (e.g. size limits), since the `for` loop makes it easy to add conditions.

## Code

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = []
        def backtracking(start, path):
            res.append(path.copy())
            
            for i in range(start, len(nums)):
                path.append(nums[i])
                backtracking(i+1, path)
                path.pop()

        backtracking(0, [])

        return res
```

## Complexity

Time: O(n · 2^n) — 2^n subsets, each copied in O(n)  
Space: O(n) — recursion stack depth
