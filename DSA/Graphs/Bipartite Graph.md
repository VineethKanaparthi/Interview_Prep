> Related to: [[Graphs]], [[BFS]]
> Reading: [cp-algorithms](https://cp-algorithms.com/graph/bipartite-check.html)
> problems: [cses-building-teams](https://cses.fi/problemset/task/1668) 

## Table of Contents

- [Summary](#Summary)

## Summary

---
> What is a bipartite graph
---
- A bipartite graph is a graph which can be divided into two disjoint sets, such that there are no edges between two nodes in the same set. (only edges to the other set)
---
> *Problem* : Given a graph, check whethere it is a bipartite graph and output the disjoint set each node belongs to
---

## Algorithm

- use bfs, assign levels.
- if an adjacent node is already visited check if its in the same set i.e., 
```C++
side[v] = level[v]%2
if(side[u]==side[v]){
	//not bipartite
}
```
- if its in the same set, the graph is not bipartite