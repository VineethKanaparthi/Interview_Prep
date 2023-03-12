> Related to [[Graphs]], [[Dijkstra's]], [[Bellman-Ford]]
> Reading : [cp-algorithms](https://cp-algorithms.com/graph/all-pair-shortest-path-floyd-warshall.html) [algo-tree](https://algotree.org/algorithms/floyd-warshall/) 
> Videos: [unacademy](https://unacademy.com/class/shortest-path-algorithms-iii-floyd-warshall-algorithm/F1AT0WT2) 

## Table of Contents

- [Summary](#Summary)
- [Implementation](#Implementation)

## Summary
----
> Why do we need another algorithm
-----
- We can find all pair from [[Dijkstra's]] in a sparse graph(no -ve weights) in `N*(E*logE + E)`  but in dense graph where E~N<sup>2</sup> the time complexity becomes N<sup>3</sup> * log(N) that too in a graph with no negative edges. If we use the plain [[Dijkstra's]] for dense graph the complexity comes down to N<sup>3</sup> (without pq or set) but again in a graph with no negative edges.
- Can we do better for graphs with negative edges? What happens if we use  [[Bellman-Ford]] ? The complexity of Bellman Ford is `N*M`. In a sparse graph, for all pair shortest paths the complexity becomes `N*N*M` and for a dense graph this will go upto N<sup>4</sup>
- Can we do better? Yes and in comes [[Floyd-Warshall]]
-----
> Algorithm Description
------
- After $k_{th}$ phase $d[i][j]$ represents the shortest distance from $i_{th}$ node to $j_{th}$ node such that only the nodes in the $set(1,2,3,4,5...k)$ are in the path from $i$ to $j$ .
- $d_{k}[i][j]$ represent the shortest distance from node $i$ to node $j$ after the $k_{th}$ phase.
- At the beginning of $k_{th}$ phase, we already have $d_{k-1}[i][j]$.
- So $d_{k}[i][j]$ is $min(d_{k-1}[i][j],  d_{k-1}[i][k] +d_{k-1}[k][j])$ 
-  $d_{0}[i][j]$ = $w_{i,j}$ *if j is an adjacent node of i*
-  $d_{0}[i][j]$ = `INF if i!=j and 0 if i == j`
- so in summary three loops for i,j and k -> 0 to n
-----
>  What about cycles?
-----
- By the end of the algorithm if there is a node x such that $d[x][x] < 0$ then there is a cycle that travels through the node x.
- Why is this so?
-  suppose there are nodes $k1, k2$ such that $d[x][k1] < 0$ and $d[k1][k2] < 0$ and $d[k2][x] < 0$ then   there is a cycle.
-  There comes a point in algo when we have to choose k1 and k2 for a path from x->x. so $d[x][x]$ will become $<0$ 
----
## Implementation

```C++
#include <bits/stdc++.h>
using namespace std;

const int INF = INT_MAX;
const int NEG_INF = INT_MIN;

class Edge{
public:
	int u,v,w;
	Edge(int u_, v_, w_): u(u_), v(v_), w(w_){}
};

floyd_warshall(vector<vector<int>>& g){
	int n = g.size();
	for(int k=0;k<n;k++){
		for(int i=0;i<n;i++){
			for(int j=0;j<n;j++){
				if(d[i][k] < INF && d[k][j] < INF){
					d[i][j] = min(d[i][j], d[i][k]+d[k][j]);
				}
			}
		}
	}
}

int main(){
	/* Construct the graph */
	int n,m;
	cin >> n >> m;
	vector<Edge> edges;
	vector<vector<int>> graph(n, vector<int>(n, INF));
	for(int i=0;i<n;i++){
		g[i][i] = 0;
	}
	for(auto edge: edges){
		g[edge.u][edge.v] = edge.w;
	}

	floyd_warshall(graph);

	// detect cycle;
	bool has_cycle = false;
	for(int i=0;i<n;i++){
		if(graph[i][i] < 0){
			has_cycle = true;
		}
	}
	// reduce all the pairs that has a path through nodes which are part of cycle
	if(has_cycle){
		for(int i=0;i<n;i++){
			for(int j=0;j<n;j++){
				for(int k=0;k<n;k++){
					if(graph[k][k]<0 && graph[i][k]<INF && graph[k][j]<INF){
						graph[i][j] = NEG_INF;
					}
				}
			}
		}
	}
	
	
}
```