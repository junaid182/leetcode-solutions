# Invert Binary Tree

**Link:** https://leetcode.com/problems/invert-binary-tree/

## Approach

**Brute force:** BFS/level-order traversal, swapping children at each node. Works but requires a queue and O(n) extra space.

**Optimized:** Recursively swap the left and right children at each node, then recurse into both subtrees. The swap happens top-down before recursing.

**Why it works:** Inverting a tree means every node's left and right children are mirrored. Swapping children at a node and then recursing into each subtree applies this transformation to the entire tree bottom-up naturally through the call stack.

## Code

```python
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return

        root.left, root.right = root.right, root.left

        self.invertTree(root.left)
        self.invertTree(root.right)

        return root
```

## Complexity

Time: O(n) — every node is visited once
Space: O(n) — call stack depth is O(h) where h is tree height; O(n) worst case for a skewed tree
