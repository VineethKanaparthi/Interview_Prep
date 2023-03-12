> related to: [[Graphs]], [[Strongly Connected Components]]
> problem: [cses-course-scheduling](https://cses.fi/problemset/task/1679/)
> reading: [usaco-guide-must-read](https://usaco.guide/gold/toposort?lang=cpp), [cp-algorithms](https://cp-algorithms.com/graph/topological-sort.html), [csacademy-for-detailed-explanation](https://csacademy.com/lesson/topological_sorting/) 

## Table of Contents

- [Summary](#Summary)
- [Algorithm](#Algorithm)

## Summary

- **DAG** - Directed Acyclic Graph is a directed graph which contains no cycles i.e., its impossible for us to start from a node and go through series of nodes and reach the starting node in a DAG.
- *Topological ordering* - A topological is a linear ordering of nodes so that  for each each edge $u->v$ , $u$ occurs before $v$ in the ordering.  
- Topological ordering maynot be unique.
- *indegree* - indegree of a node is the number of edges coming into the node.
- *outdegree* - outdegree of a node is the number of edges originating from the node.
- use -*DFS* method if you are unsure about whether graph is cyclic or not.

## Algorithm

1. Find a node with *indegree* $0$ else exit.
2. Remove that node from the graph
3. Go to step 1
