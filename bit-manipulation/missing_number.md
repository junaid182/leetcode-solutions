# Missing Number

**Link:** https://leetcode.com/problems/missing-number/

## Approach

XOR every index `i` (0 to n-1) with every value `nums[i]`, starting from `res = n`. Each number that's present cancels out its matching index (`x ^ x = 0`), leaving only the missing number.

**Why it works:** We're XOR-ing the set `{0, 1, ..., n}` against `{nums[0], ..., nums[n-1]}`. Every value except the missing one appears in both sets and cancels, leaving the missing number.

## Code

```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        res = len(nums)

        for i in range(len(nums)):
            res ^= i ^ nums[i]
        
        return res
```

## Complexity

Time: O(n) — single pass  
Space: O(1)
