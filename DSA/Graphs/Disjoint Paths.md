> related to: [[Graphs]], [[Max Flow]]
> reading: [[CPH.pdf|CPH Page 196]] 

## Table of Contents

- [[Disjoint Paths#Edge Disjoint Paths|Edge Dijsoint Paths]] 
- [[Disjoint Paths#Node Disjoint Paths|Node Dijsoint Paths]]


## Edge Disjoint Paths

> What are **edge-disjoint** paths?
>  Set of paths such that each edge appears in at most one path

**It turns out that maximum number if edge disjoint paths equals to the maxflow of the graph, assuming that the capacity of each edge is one**

> After the max flow has been constructed, the edge-disjoint paths can be found greedily by following paths from source to sink.

## Node Disjoint Paths

> What are node dijsoint paths?
> every node except the source and sink may appear in at most one path.

> The number of node disjoint paths maybe smaller than the number of edge disjoint paths


**We can reduce this problem to max flow problem. Divide each node into two nodes such that one node has incoming edges and the other node has outgoing edges and add a new edge from first node to second node.**


