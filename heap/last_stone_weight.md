# Last Stone Weight

**Link:** https://leetcode.com/problems/last-stone-weight/

## Approach

**Brute force:** Sort the list on every iteration, smash the two heaviest, repeat until one or zero stones remain.

**Optimized:** Use a max-heap (simulated with negated values in Python's min-heap) to always efficiently access the two heaviest stones. Pop the two largest, push back the difference if nonzero, and repeat until one or fewer stones remain.

**Why it works:** A max-heap gives O(log n) access to the largest element at each step, avoiding an O(n log n) re-sort every iteration. Negating values lets Python's `heapq` (min-heap) act as a max-heap.

## Code

```python
class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        stones = [-s for s in stones]
        heapq.heapify(stones)

        while len(stones) > 1:
            first = heapq.heappop(stones)
            second = heapq.heappop(stones)

            if second > first:
                heapq.heappush(stones, first - second)
        
        stones.append(0)
        return abs(stones[0])
```

## Complexity

Time: O(n log n)  
Space: O(n)
