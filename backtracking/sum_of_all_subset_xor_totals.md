# Sum of All Subset XOR Totals

**Link:** https://leetcode.com/problems/sum-of-all-subset-xor-totals/

## Approach

**Backtracking (DFS):** At each index, branch into two choices — take the element (XOR it into the running value) or skip it. When all elements are exhausted, return the accumulated XOR. Sum all leaf values as we unwind.

**Why it works:** Every subset is visited exactly once via the take/skip binary tree. The base case returns the XOR total for that subset, and summing `take + skip` at each node accumulates the answer over all subsets without needing to store them explicitly.

## Code

```python
class Solution:
    def subsetXORSum(self, nums: List[int]) -> int:

        def dfs(i, total):
            if i == len(nums):
                return total
            
            return dfs(i+1, total ^ nums[i]) + dfs(i+1, total)
        
        return dfs(0, 0)
```

## Complexity

Time: O(2^n)  
Space: O(n) — recursion stack depth
