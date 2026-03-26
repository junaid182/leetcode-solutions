# Binary Tree Preorder Traversal

**Link:** https://leetcode.com/problems/binary-tree-preorder-traversal/

## Approach

**Brute force:** N/A — recursion is the natural solution for tree traversal.

**Optimized:** Use a recursive helper that follows node → left → right order (preorder). Results are collected into a shared list via closure.

**Why it works:** Preorder traversal visits the current node first before descending into subtrees. This naturally produces a top-down ordering of nodes.

## Code

```python
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = []

        def preorder(root):
            if not root:
                return

            res.append(root.val)
            preorder(root.left)
            preorder(root.right)

        preorder(root)

        return res
```

## Complexity

Time: O(n) — every node is visited once
Space: O(n) — call stack depth is O(h) where h is tree height; O(n) worst case for a skewed tree
