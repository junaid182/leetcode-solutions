# Letter Combinations of a Phone Number

**Link:** https://leetcode.com/problems/letter-combinations-of-a-phone-number/

## Approach

Backtracking over each digit's mapped characters. Maintain an outer `path` list. At each index `i`, try appending every letter mapped to `digits[i]`, recurse to the next digit, then pop (backtrack). When `i` reaches the end, join `path` and record it.

## Code

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:

        digitsToChar = {
            "2": "abc",
            "3": "def",
            "4": "ghi",
            "5": "jkl",
            "6": "mno",
            "7": "pqrs",
            "8": "tuv",
            "9": "wxyz"
        }

        res = []

        def backtrack(start, path):
            if start == len(digits):
                res.append("".join(path))
                return
            
            for ch in digitsToChar[digits[start]]:
                path.append(ch)
                backtrack(start+1, path)
                path.pop()

        backtrack(0, [])

        return res
```

## Complexity

Time: O(4^n · n) — at most 4 letters per digit, n digits, each combination takes O(n) to build  
Space: O(n) — recursion depth
