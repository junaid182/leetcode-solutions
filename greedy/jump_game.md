# Jump Game

**Link:** https://leetcode.com/problems/jump-game/

## Approach

Work backwards. Start with `goal` at the last index. For each position `i`, if `i + nums[i] >= goal`, then `i` can reach the goal — shift `goal` back to `i`. If `goal` reaches `0`, every position along the way can chain to the end.

**Why it works:** Greedily shrinking the goal leftward avoids tracking all possible jump paths. If any position can reach the current goal, it becomes the new target.

## Code

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        goal = len(nums) - 1

        for i in range(len(nums)-1, -1, -1):
            if i + nums[i] >= goal:
                goal = i
        
        return True if goal == 0 else False
```

## Complexity

Time: O(n) — single backwards pass  
Space: O(1)
