> Related to : [[Graphs]], [[DFS]], [[BFS]] 
> Reading: [cp-algorithms](https://cp-algorithms.com/graph/search-for-connected-components.html)

## Table of Contents

- [key points](#Key-Points)
- [Algorithm](#Algorithm)
- [Implementation](#Implementation)
---
### Key-Points
---
- Connected component: A sub-set of vertices in a graph such that any two nodes in the graph can be reached from one another.
---
### Algorithm
----
- We can use either [[DFS]] or [[BFS]]
- Apply [[DFS]] or [[BFS]] multiple times as long as there are unvisited vertices.
- We can store the components of a CC in an array
----
### Implementation

```C++
for(int i=0;i<n;i++){
	if(!visited[i]){
		dfs(graph, i, visited);
	}
}
```