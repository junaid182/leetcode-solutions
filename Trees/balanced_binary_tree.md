# Balanced Binary Tree

**Link:** https://leetcode.com/problems/balanced-binary-tree/

## Approach

**Brute force:** For each node, compute the height of its left and right subtrees separately and check if the difference exceeds 1. Recurse for every node. O(n²) because height is recomputed from scratch at each node.

**Optimized:** Single DFS that computes height bottom-up. At each node, check if `abs(leftHeight - rightHeight) > 1` and flip a `result` flag to `False` if so. Return `1 + max(leftHeight, rightHeight)` to the parent as usual, letting the height propagate up while the balance check runs in the same pass.

**Why it works:** A tree is balanced only if every subtree is balanced. By computing heights bottom-up in one DFS and checking the balance condition at every node, we detect any violation in a single traversal without redundant height computations.

## Code

```python
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        res = True

        def dfs(cur):
            if not cur:
                return 0

            left = dfs(cur.left)
            right = dfs(cur.right)

            if abs(right - left) > 1:
                nonlocal res
                res = False

            return 1 + max(left, right)

        dfs(root)

        return res
```

## Complexity

Time: O(n) — every node is visited once
Space: O(n) — call stack depth is O(h); O(n) worst case for a skewed tree
