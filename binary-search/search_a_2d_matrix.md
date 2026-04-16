# Search a 2D Matrix

**Link:** https://leetcode.com/problems/search-a-2d-matrix/

## Approach

**Brute force:** Scan every element in the matrix — O(m * n).

**Optimized:** Two binary searches. First, binary search the rows by comparing the target against each row's first and last element to find which row could contain the target. Then binary search within that row.

**Why it works:** Each row is sorted, and the first element of each row is greater than the last element of the previous row. This means we can treat row selection as a binary search problem — eliminate the top or bottom half of rows based on boundary comparisons, then do a standard binary search inside the identified row.

## Code

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        top, bot = 0, len(matrix) - 1
        row = 0

        while top <= bot:
            mid = (top + bot) // 2

            if target >= matrix[mid][0] and target <= matrix[mid][-1]:
                row = mid
                break
            elif target < matrix[mid][0]:
                bot = mid - 1
            else:
                top = top + 1

        left, right = 0, len(matrix[row]) - 1

        while left <= right:
            mid = (left + right) // 2

            if target == matrix[row][mid]:
                return True
            elif target < matrix[row][mid]:
                right = mid - 1
            else:
                left = mid + 1

        return False
```

## Complexity

Time: O(log m + log n)
Space: O(1)
