# Clone Graph

**Link:** https://leetcode.com/problems/clone-graph/

## Approach

DFS with a hashmap (`oldToNew`) mapping each original node to its clone. Before recursing into neighbors, register the clone immediately — this handles cycles by returning the already-created clone if a node is visited again.

## Code

```python
class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:

        oldToNew = {}

        def dfs(node):

            if not node:
                return

            if node in oldToNew:
                return oldToNew[node]
            
            copy = Node(node.val)
            oldToNew[node] = copy

            for neighbor in node.neighbors:
                copy.neighbors.append(dfs(neighbor))
            
            return copy

        return dfs(node)
```

## Complexity

Time: O(V + E) — each node and edge visited once  
Space: O(V) — hashmap and recursion stack
