# Kth Largest Element in a Stream

**Link:** https://leetcode.com/problems/kth-largest-element-in-a-stream/

## Approach

Maintain a min-heap capped at size `k`. The heap's minimum (`minheap[0]`) is always the kth largest — every element smaller than it has been evicted.

On initialization, heapify the input and pop until the heap has exactly `k` elements. On each `add`, push the new value and pop the minimum if the heap exceeds size `k`. The root is always the answer.

## Code

```python
class KthLargest:

    def __init__(self, k: int, nums: List[int]):
        self.minheap, self.k = nums, k
        heapq.heapify(self.minheap)
        while len(self.minheap) > self.k:
            heapq.heappop(self.minheap)

    def add(self, val: int) -> int:
        heapq.heappush(self.minheap, val)
        if len(self.minheap) > self.k:
            heapq.heappop(self.minheap)
        return self.minheap[0]
```

## Complexity

Time: O(n log n) for `__init__`, O(log k) per `add`  
Space: O(k) — heap is capped at k elements
