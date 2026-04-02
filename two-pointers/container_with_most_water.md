# Container With Most Water

**Link:** https://leetcode.com/problems/container-with-most-water/

## Approach
**Brute force:** Check every pair of lines and compute the area between them. This gives O(n²) time.

**Optimized:** Use two pointers starting at both ends. At each step, compute the area using the shorter line as height and the gap as width. Move the pointer pointing to the shorter line inward — keeping the taller line gives the best chance of finding a larger area with a smaller width.

**Why it works:** The area is bounded by the shorter line, so moving the shorter pointer is the only way to potentially increase height. Moving the taller pointer can only decrease or maintain width while never increasing height, so it can never produce a better result.

## Code
```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        l, r = 0, len(height) - 1
        maxArea = 0

        while l < r:
            w = r - l
            h = min(height[l], height[r])
            maxArea = max(maxArea, w * h)
            if height[l] < height[r]:
                l += 1
            else:
                r -= 1

        return maxArea
```

## Complexity
Time: O(n)
Space: O(1)
