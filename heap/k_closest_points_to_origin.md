# K Closest Points to Origin

**Link:** https://leetcode.com/problems/k-closest-points-to-origin/

## Approach

**Brute force:** Compute distances for all points, sort by distance, return first k.

**Optimized:** Build a min-heap of all points keyed by squared Euclidean distance, then pop k times. Avoids sorting the full list — we only extract what we need.

**Why it works:** Heapifying is O(n), and each pop is O(log n), so we pay O(n + k log n) instead of O(n log n) for a full sort. Using squared distance avoids the sqrt computation without affecting ordering.

## Code

```python
class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        distHeap = []

        for x, y in points:
            dist = (x ** 2) + (y ** 2)
            distHeap.append([dist, x, y])
        
        heapq.heapify(distHeap)

        res = []
        while k > 0:
            dist, x, y = heapq.heappop(distHeap)
            res.append([x, y])
            k -= 1
        
        return res
```

## Complexity

Time: O(n + k log n)  
Space: O(n)
