# Count Connected Components in an Undirected Graph

**Link:** https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/

## Approach

Build an undirected adjacency list. Iterate over all nodes — each unvisited node starts a new component. DFS from it to mark the entire connected component as visited.

## Code

```python
class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        graph = defaultdict(list)

        for v1, v2 in edges:
            graph[v1].append(v2)
            graph[v2].append(v1)
        
        path = set()
        visited = set()

        def dfs(v):
            if v in path:
                return
            
            if v in visited:
                return
            
            path.add(v)
            for ver in graph[v]:
                dfs(ver)
            path.remove(v)
            visited.add(v)

        components = 0
        for v in range(n):
            if v not in visited:
                dfs(v)
                components += 1

        return components
```

## Complexity

Time: O(V + E) — each node and edge visited once  
Space: O(V + E) — adjacency list and visit set
