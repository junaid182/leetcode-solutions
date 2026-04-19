# Kth Smallest Element in a BST

**Link:** https://leetcode.com/problems/kth-smallest-element-in-a-bst/

## Approach

**Brute force:** Do a full inorder traversal, collect all values into a sorted list, return the k-th element.

**Optimized:** Iterative inorder traversal using an explicit stack. In a BST, inorder traversal visits nodes in ascending order. We traverse left as far as possible, then process the node, then move right — incrementing a counter each time we pop. When the counter reaches k, we've found the k-th smallest.

**Why it works:** BST inorder traversal produces values in sorted ascending order. Stopping early at the k-th visit avoids processing the rest of the tree.

## Code

```python
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        cur = root
        stack = []
        n = 0

        while cur or stack:
            while cur:
                stack.append(cur)
                cur = cur.left
            
            cur = stack.pop()
            n += 1
            if n == k:
                return cur.val
            
            cur = cur.right
```

## Complexity

Time: O(H + k) where H is the height of the tree  
Space: O(H) for the stack
