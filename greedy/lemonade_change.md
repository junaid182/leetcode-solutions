# Lemonade Change

**Link:** https://leetcode.com/problems/lemonade-change/

## Approach

Track counts of $5 and $10 bills on hand (since $20 bills are useless for making change). For each customer:
- **$5 bill:** no change needed, just pocket it.
- **$10 bill:** give back one $5.
- **$20 bill:** greedily prefer $10 + $5 over three $5s, since $5 bills are more versatile.

Return `False` as soon as change can't be made.

## Code

```python
class Solution:
    def lemonadeChange(self, bills: List[int]) -> bool:
        five, ten = 0, 0

        for b in bills:
            if b == 5:
                five += 1
            elif b == 10:
                if five == 0:
                    return False
                five -= 1
                ten += 1
            else:  # b == 20
                if ten > 0 and five > 0:
                    ten -= 1
                    five -= 1
                elif five >= 3:
                    five -= 3
                else:
                    return False

        return True
```

## Complexity

Time: O(n) — single pass through bills  
Space: O(1) — only two counters maintained
