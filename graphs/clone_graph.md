# Clone Graph

**Link:** https://leetcode.com/problems/clone-graph/

## Approach

DFS with a hashmap (`oldToNew`) mapping each original node to its clone. Before recursing into neighbors, register the clone immediately — this handles cycles by returning the already-created clone if a node is visited again.

## Code

```python
class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:

        if not node:
            return None

        graph = {}

        def dfs(node):
            if node in graph:
                return graph[node]

            copy = Node(node.val)
            graph[node] = copy

            for nei in node.neighbors:
                copy.neighbors.append(dfs(nei))
            
            return copy


        return dfs(node)
```

## Complexity

Time: O(V + E) — each node and edge visited once  
Space: O(V) — hashmap and recursion stack
