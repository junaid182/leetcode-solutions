# Maximum Subarray

**Link:** https://leetcode.com/problems/maximum-subarray/

## Approach

Kadane's algorithm: maintain a running sum `curSum`. If it drops negative, reset it to zero — a negative prefix can only hurt any future subarray. Add each element and track the global maximum.

**Why it works:** At every position, `curSum` holds the maximum subarray sum ending at that index. Resetting on negative is equivalent to starting a new subarray from the current element.

## Code

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        maxSum = nums[0]
        curSum = 0

        for n in nums:
            if curSum < 0:
                curSum = 0
            curSum += n
            maxSum = max(maxSum, curSum)
        
        return maxSum
```

## Complexity

Time: O(n) — single pass  
Space: O(1)
