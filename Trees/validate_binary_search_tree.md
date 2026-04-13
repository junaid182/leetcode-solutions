# Validate Binary Search Tree

**Link:** https://leetcode.com/problems/validate-binary-search-tree/

## Approach

**Brute force:** In-order traversal produces a sorted sequence for a valid BST — check that the resulting list is strictly increasing. O(n) time and O(n) space for the list.

**Optimized:** DFS passing down a valid range `(left, right)` for each node. A node is valid only if its value falls strictly within that range. Recurse left with the upper bound tightened to `node.val`, and right with the lower bound tightened to `node.val`.

**Why it works:** The BST property isn't just about a node and its direct children — every node in the left subtree must be less than all ancestors where we turned right, and vice versa. Propagating the bounds captures this global constraint rather than just checking immediate parent-child relationships.

## Code

```python
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:

        def valid(node, left, right):
            if not node:
                return True
            if not (node.val > left and node.val < right):
                return False

            return (valid(node.left, left, node.val) and
                    valid(node.right, node.val, right))

        return valid(root, float("-inf"), float("inf"))
```

## Complexity

Time: O(n)  
Space: O(h) where h is the height of the tree (O(log n) balanced, O(n) worst case)
