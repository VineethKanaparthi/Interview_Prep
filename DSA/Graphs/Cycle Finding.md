> related to [[Graphs]], [[DFS]], [[Bellman-Ford]], [[Floyd-Warshall]]
> reading: [cp-algorithms](https://cp-algorithms.com/graph/finding-cycle.html)
> problems: [cses-round-trip](https://cses.fi/problemset/task/1669), [cses-cycle-finding](https://cses.fi/problemset/task/1197), [cses-round-trip-ii](https://cses.fi/problemset/task/1678) 

## Table of Contents

- [finding a cycle](#Finding_Cycles)
- [finding a negative cycle](#negative_cycle)

## Finding_Cycles

---
>problem: Given a directed/undirected graph, find if a cycle exists and if it exists print the path of a cycle.
---
- We can solve this using DFS.
- We will run a series of DFS and track the parents using a parent array
- Intially color of all the vertices =`0`
- Once we visit them the color changes to `1`
- When we exit them the color changes to `2`
- In a directed graph if there is an edge from the node we are visiting to a node with color `1`. There exists a cycle.
- If there is an edge from node `u` to a node `v` with color `2` that means `u` is not a direct descendant of `v`
- once we find a cycle, we can reconstruct it using the parent array.

## negative_cycle

---
>problem: You are given a directed weighted graph   $G$  with   $N$  vertices and   $M$  edges. Find any cycle of negative weight in it, if such a cycle exists. 
--- 
- use [[Bellman-Ford]]
---
> problem: find all pairs of vertices which have a path of arbitrarily small weight between them.
---
- use [[Floyd-Warshall]]