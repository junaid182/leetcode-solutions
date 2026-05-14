# Letter Combinations of a Phone Number

**Link:** https://leetcode.com/problems/letter-combinations-of-a-phone-number/

## Approach

Backtracking over each digit's mapped characters. At each index `i`, try appending every letter mapped to `digits[i]` and recurse to the next digit. When the built string length equals the input length, record it.

Note: if `digits` is empty, `backtracking(0, "")` hits the base case immediately and appends `""` — but since `res` starts empty and we never call the function when `digits` is empty... actually the function is always called, so an empty `digits` input returns `[""]`. LeetCode expects `[]` for empty input, so a guard `if not digits: return []` before calling `backtracking` would be safer.

## Code

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        res = []
        digitToChar = {
            "2" : "abc",
            "3" : "def",
            "4" : "ghi",
            "5" : "jkl",
            "6" : "mno",
            "7" : "pqrs",
            "8" : "tuv",
            "9" : "wxyz",
        }

        def backtracking(i, curStr):
            if len(curStr) == len(digits):
                res.append(curStr)
                return
            
            for c in digitToChar[digits[i]]:
                backtracking(i+1, curStr+c)

        backtracking(0, "")

        return res
```

## Complexity

Time: O(4^n · n) — at most 4 letters per digit, n digits, each combination takes O(n) to build  
Space: O(n) — recursion depth
