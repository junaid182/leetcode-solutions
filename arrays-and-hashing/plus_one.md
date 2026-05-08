# Plus One

**Link:** https://leetcode.com/problems/plus-one/

## Approach

Reverse the array to process least-significant digits first. Carry starts at `1` (the +1 to add). Iterate with a carry: if the current digit is `9`, set it to `0` and keep carry; otherwise increment and clear carry. If the index goes out of bounds, append `1` (a new most-significant digit). Reverse back before returning.

## Code

```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        digits = digits[::-1]

        carry = 1
        index = 0 

        while carry:
            if index < len(digits):
                if digits[index] == 9:
                    digits[index] = 0
                    carry = 1
                else:
                    digits[index] += 1
                    carry = 0
            
            else:
                digits.append(1)
                carry = 0
            index += 1
        
        return digits[::-1]
```

## Complexity

Time: O(n) — single pass through digits  
Space: O(n) — reversed copy of the array
