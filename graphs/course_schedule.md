# Course Schedule

**Link:** https://leetcode.com/problems/course-schedule/

## Approach

Build an adjacency list of prerequisites. DFS each course to check for cycles. `path` tracks the current DFS path — if we revisit a node on the same path, there's a cycle. After confirming a course is completable, clear its prerequisites list so future DFS calls on it return immediately (memoization).

**Why it works:** A cycle in the prerequisite graph means some course depends on itself transitively, making it impossible to complete. Clearing `graph[crs]` after a successful traversal avoids redundant work.

## Code

```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        graph = defaultdict(list)

        for course, pre in prerequisites:
            graph[course].append(pre)
        
        visited = set()
        def dfs(crs):
            if crs in visited:
                return False
            
            if graph[crs] == []:
                return True
            
            visited.add(crs)
            for course in graph[crs]:
                if not dfs(course):
                    return False
            visited.remove(crs)
            graph[crs] = []

            return True


        for crs in range(numCourses):
            if not dfs(crs):
                return False
        
        return True
```

## Complexity

Time: O(V + E) — each course and prerequisite edge visited once  
Space: O(V + E) — adjacency list and recursion stack
