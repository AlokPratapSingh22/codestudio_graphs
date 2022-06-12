## Course Schedule (Imp)

- #### [Leetcode](https://leetcode.com/problems/course-schedule/)
- #### [CodeStudio](https://www.codingninjas.com/codestudio/library/course-schedule)

### Problem Statement

You are a student of Netaji Subhas Institute of Technology. You have to take ‘N’ number of courses labelled from 1 to N to complete your B.Tech Degree.
Some courses may have prerequisites, for example, to take course 1 you have to first take course 2, which is expressed as a pair: [1, 2]. Now, your task is to find is it possible for you to finish all courses.
Note: There are no duplicate pairs in the prerequisites array.
**For Example-**
If N = 2 and prerequisite = [[1, 2]]. Then, there are a total of 2 courses you need to take. To take course 1 you need to finish course 2. So, it is possible to complete all courses.

### Solution

First create a graph from the given pre-requisites considering them as edges.

- The brute-force approach might be traversing the created graph and checking the possibility if all courses (vertices) can be reached or completed

- The best or optimized approach would be to use **Kadane's Algo** or **Topological Sorting**, as we need the best way in which we can reach all the vertices of our graph, which is exactly what the topo sort does.

### Code

#### For Leetcode

```Python
def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        courses = {i:[] for i in range(numCourses)}

        for i, j in prerequisites:
            courses[i].append(j)

        visited = set()
        def dfs(courses, src):
            if src in visited:
                return False

            if len(courses[src]) == 0:
                return True
            visited.add(src)
            for j in courses[src]:
                if not dfs(courses, j):
                    return False
            visited.remove(src)
            courses[src] = []
            return True
        for c in courses:
            if not dfs(courses, c):
                return False
        return True
```

#### Codestudio

```Python
def canFinish(prerequisites, n, m):
    adj = {i:[] for i in range(1,n+1)}
    inorder = {i:0 for i in range(1,n+1)}

    for u, v in prerequisites:
        adj[u].append(v)
        inorder[v]+=1
    q = []
    for i in range(1, n+1):
        if inorder[i] == 0:
            q.append(i)
    res = []
    while q:
        u = q.pop(0)
        res.append(u)
        for v in adj[u]:
            inorder[v] -= 1
            if inorder[v] == 0:
                q.append(v)

    if len(res) == n:
        return "Yes"
    return "No"

```
