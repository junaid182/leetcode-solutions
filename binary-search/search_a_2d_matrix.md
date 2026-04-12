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
        ROWS, COLS = len(matrix), len(matrix[0])

        top, bot = 0, ROWS - 1

        while top <= bot:
            Row = (top + bot) // 2

            if target < matrix[Row][0]:
                bot = bot - 1
            elif target > matrix[Row][-1]:
                top = top + 1
            else:
                break

        if not (top <= bot):
            return False

        Row = (top + bot) // 2
        l, r = 0, COLS - 1

        while l <= r:
            m = (l + r) // 2

            if target < matrix[Row][m]:
                r = r - 1
            elif target > matrix[Row][m]:
                l = l + 1
            else:
                return True

        return False
```

## Complexity

Time: O(log m + log n)
Space: O(1)
