# Kth Largest Element in an Array

**Link:** https://leetcode.com/problems/kth-largest-element-in-an-array/

## Approach

**Optimized:** Negate all values and heapify into a min-heap, which simulates a max-heap. Pop k-1 times to discard the largest elements, then the top holds the kth largest (negated).

**Why it works:** Python's `heapq` is a min-heap, so negating values lets us treat the smallest negated value as the largest original value. We only need k-1 pops rather than sorting the entire array.

## Code

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        minHeap = [-n for n in nums]
        heapq.heapify(minHeap)

        while k > 1:
            heapq.heappop(minHeap)
            k -= 1
        
        return -minHeap[0]
```

## Complexity

Time: O(n + k log n)  
Space: O(n)
