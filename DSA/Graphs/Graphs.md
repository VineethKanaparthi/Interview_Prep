> related to: [[DSA Prep]]
> resources: [usaco-guide](https://usaco.guide/), [cp-algorithms](https://cp-algorithms.com/graph/breadth-first-search.html)
> videos:  [SPA Course](https://unacademy.com/a/free-course-on-shortest-path-algorithms),  [Triveni Mahata Unacademy](https://unacademy.com/a/free-course-on-graph-algorithms-new) ,   [CodeNCode 1](https://www.youtube.com/watch?v=s7zE4Nmc2Fg&list=PL5DyztRVgtRVLwNWS7Rpp4qzVVHJalt22),  [CodeNCode 2](https://www.youtube.com/watch?v=eaD68J3NNdE&list=PL5DyztRVgtRW0Kdd8i1xML7t-ge56XRQR)


## Table of Contents

- [To-Do](#To-Do)
- [Sub Topics](##Topics)
- [Open Questions](#Open-Questions)
- [Representation](##Representation)

## To-Do


Easy
- [x] [[Strongly Connected Components]]
- [ ] [[Max Flow]]

Medium
- [x] [[Eulerain Path]] (!practice again)

Hard
- [ ] Maximum Matching
- [ ] [[Successor Graphs]]
- [ ] Binary Jumping
- [ ] [[Hamiltonian Path]]
- [ ] LCA
- [ ] [[Disjoint Paths]]
- [ ] Path Covers

## Topics

 - [x] [[Union find]]
 - [x] Graph Traversal ([[BFS]], [[DFS]])
 - [x] [[BFS#Multi-Source-BFS|Multi-Source BFS]]
 - [x] [[Bipartite Graph]]
 - [x] Single Source Shortest Path ([[Dijkstra's]], [[Bellman-Ford]])
 - [x] All pair Shortest Path ([[Floyd-Warshall]])
 - [x] DAG
	 - [x] [[Topological Ordering]]
	 - [x] [[DP on DAG]]
	 - [x] [[Dijkstra's#Dijkstras-DAG|Shortest Path DAG]]
 - [ ] [[Successor Graphs]] (**Read again and again and again**)
 - [ ] CC, SCC
	 - [x] [[Connected Components]]
	 - [x] [[Strongly Connected Components]]
	 - [x] Condensation Graph
	 - [ ] Strong Orientation
 - [ ] [[Bridges]] , [[Articulation Points]]
 - [x] Graph on 2D  ([[Graph on 2D Grid]])
 - [ ] Cycles 
	 - [x] [[Cycle Finding#Finding_Cycles|Detecting cycle using DFS]]
	 - [x] [[Cycle Finding#negative_cycle|Detecting negative cycle using bellman ford]]
	 - [x] [[Cycle Finding#negative_cycle|Detecting all pair -inf paths using floyd-warshall]]
	 - [x] [[Eulerain Path]] (!practice again)
	 - [ ] [[Hamiltonian Path]]
 - [x] MST ([[Prims]], [[Kruskals]])
 - [ ] LCA
 - [ ] Flows and Cuts
	 - [ ] [[Max Flow|Max Flow and Minimum Cut]]
	 - [ ] [[Disjoint Paths]]
	 - [ ] [[Maximum Matching]]
	 - [ ] Path Covers


## Representation
#### Adj Matrix
```C++
vector<vector<int>> g(n, vector<int>(n,0));
int g[n][n];
```

#### Adj List
```C++
func(vector<vector<int>>& g)
vector<vector<int>> g(n);
func(vector<int> g[n])
vector<int> g[n];
```

#### Edge List
```C++
class Edge{
	int u,v,w;
public:
	Edge(int u_, int v_, int w_): u(u_),v(v_),w(w_){
	}
}

int main(){
	vector<Edge> edgeList(e);
}
```
## Open-Questions

- [ ] how is topological ordering related to SCC kosarajus algorithm