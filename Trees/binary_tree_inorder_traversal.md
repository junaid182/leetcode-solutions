# Binary Tree Inorder Traversal

**Link:** https://leetcode.com/problems/binary-tree-inorder-traversal/

## Approach

**Brute force:** N/A — recursion is already the natural solution for tree traversal.

**Optimized:** Use a recursive helper that follows left → node → right order (inorder). Results are collected into a shared list via closure.

**Why it works:** Inorder traversal visits the left subtree first, then the current node, then the right subtree. Recursion naturally mirrors the tree's structure, unwinding back up the call stack in the correct order.

## Code

```python
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = []

        def inorder(curr):
            if not curr:
                return
            inorder(curr.left)
            nonlocal res
            res.append(curr.val)
            inorder(curr.right)

        inorder(root)

        return res
```

## Complexity

Time: O(n) — every node is visited once
Space: O(n) — call stack depth is O(h) where h is tree height; O(n) worst case for a skewed tree
