# Kth Largest Element in an Array

**Link:** https://leetcode.com/problems/kth-largest-element-in-an-array/

## Approach

**Optimized:** Negate all values and heapify into a min-heap, which simulates a max-heap. Pop k-1 times to discard the largest elements, then the top holds the kth largest (negated).

**Why it works:** Python's `heapq` is a min-heap, so negating values lets us treat the smallest negated value as the largest original value. We only need k-1 pops rather than sorting the entire array.

## Code

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        nums = [-n for n in nums]
        heapq.heapify(nums)

        res = 0
        while k > 0:
            res = heapq.heappop(nums)
            k -= 1
        
        return -res
```

## Complexity

Time: O(n + k log n)  
Space: O(n)
