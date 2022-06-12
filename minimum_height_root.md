## [Roots of the tree having minimum height](https://www.codingninjas.com/codestudio/problems/roots-of-the-tree-having-minimum-height_1235193?topList=top-graphs-interview-questions)

===

Problem Statement
You are given an undirected Tree having 'N' nodes. The nodes are numbered from 1 to 'N'. Your task is to find the sorted list of all such nodes, such that rooting the tree on that node gives the minimum height possible of the given tree.
A tree is a connected acyclic graph. The height of a rooted tree is the maximum value of the distance between the root and all nodes of the tree.

```Python
from collections import defaultdict
def minHeightRoots(edges):
    # find the centroid and make it root
    adj = defaultdict(list)
    n = 0
    if len(edges)==0:
        return [1]
    for u,v in edges:
        adj[u].append(v)
        adj[v].append(u)
        n = max(n, u, v)

    q = []
    if n <=2:
        return [i for i in range(1,n+1)]
    for i in range(1,n+1):
        if len(adj[i]) == 1:
            q.append(i)

    rem_nodes = n

    while rem_nodes > 2:
        rem_nodes -= len(q)
        new_q = []

        while q:
            u = q.pop()
            v = adj[u].pop()
            adj[v].remove(u)

            if len(adj[v]) == 1:
                new_q.append(v)

        q = new_q
    q.sort()
    return q

```
