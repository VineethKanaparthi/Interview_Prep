> related to: [[Graphs]], [[Bipartite Graph]]

## Problem

- Find a maximum size set of node pairs in an undirected graph such that each pair is connected with an edge and each node belongs to atmost one pair.
- For bipartite graphs we can reduce this problem to maximum flow
- Just add 2 more nodes (source and sink)
	- Add edges from source to set1
	- Add edges from set2 to sink
	- Find max flow.