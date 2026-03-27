# Same Tree

**Link:** https://leetcode.com/problems/same-tree/

## Approach

**Brute force:** Serialize both trees (e.g. via inorder traversal) into arrays and compare. Works but requires extra space and multiple passes.

**Optimized:** Simultaneous recursive DFS on both trees. At each step: if both nodes are null, return True. If only one is null, return False. If values differ, return False. Otherwise recurse on both left and right subtrees and AND the results.

**Why it works:** Two trees are identical if and only if their roots match and their left and right subtrees are identical. The three base cases handle all structural/value mismatches, and the recursion checks every corresponding pair of nodes in one pass.

## Code

```python
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        if not p and not q:
            return True

        if not p or not q:
            return False

        if p.val != q.val:
            return False

        left = self.isSameTree(p.left, q.left)
        right = self.isSameTree(p.right, q.right)

        return left and right
```

## Complexity

Time: O(n) — every node pair is visited once, where n is the smaller tree's size
Space: O(n) — call stack depth is O(h); O(n) worst case for a skewed tree
