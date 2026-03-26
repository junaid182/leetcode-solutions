# Binary Tree Postorder Traversal

**Link:** https://leetcode.com/problems/binary-tree-postorder-traversal/

## Approach

**Brute force:** N/A — recursion is the natural solution for tree traversal.

**Optimized:** Use a recursive helper that follows left → right → node order (postorder). Results are collected into a shared list via closure.

**Why it works:** Postorder traversal processes both subtrees before the current node. This produces a bottom-up ordering, which is useful for operations that depend on children being handled before their parent (e.g., deletion, expression evaluation).

## Code

```python
class Solution:
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = []

        def postorder(root):
            if not root:
                return

            postorder(root.left)
            postorder(root.right)
            res.append(root.val)

        postorder(root)

        return res
```

## Complexity

Time: O(n) — every node is visited once
Space: O(n) — call stack depth is O(h) where h is tree height; O(n) worst case for a skewed tree
