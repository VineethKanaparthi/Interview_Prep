> Implementation: [cp-algorithms](https://cp-algorithms.com/graph/bellman_ford.html#a-better-implementation) [algo-tree](https://algotree.org/algorithms/single_source_shortest_path/bellman_ford_shortest_path/)
> Related: [[Dijkstra's]] , [[Graphs]], [[Floyd-Warshall]], [[Cycle Finding]]

## Table of Contents

- [Key Points](#Key-Points)
- [Proof](#Proof)
- [Implementation-Pitfalls](#Implementation-Pitfalls)
- [Implementation](#Implementation)


## Key-Points

- Bellman-Ford algorithm finds the shortest path ( in terms of distance / cost ) from a single source in a *directed, weighted graph* containing *positive and negative* edge weights.
- Unlike the [[Dijkstra's]] algorithm, this algorithm can also be applied to [[Graphs]] containing negative weight edges.
- However, if the graph contains a *negative cycle*, then, clearly, the shortest path to some vertices may not exist (due to the fact that the weight of the shortest path must be equal to minus infinity)
- This algorithm *can be modified to* signal the presence of a cycle of negative weight, or even *deduce this cycle*.


## Proof

> Asserition: After the execution of   $i_{th}$  phase, the Bellman-Ford algorithm correctly finds all shortest paths whose number of edges does not exceed   $i$ .

- In other words, for any vertex $a$  let us denote the   $k$  number of edges in the shortest path to it (if there are several such paths, you can take any). According to this statement, the algorithm guarantees that after $k_{th}$ phase the shortest path for vertex  $a$  will be found.
-  [proof](https://cp-algorithms.com/graph/bellman_ford.html#the-proof-of-the-algorithm) 

## Implementation-Pitfalls

> Avoiding overflow.

- use a `inf` which can never be added upto for distance array
- for example if max_weight of an edge is $10^9$  and there are $5000$ edges the distance can go up to $5*10^{13}$ . so choose an `inf`  $>5*10^{13}$
- second more general tip is use a function of to check if addition is overflowing (see [[C++ Tips Tricks && Tricky Things]])
```C++
long inf = 1L<<46; // 7*10^13
```

## Implementation

```c++
#include <bits/stdc++.h>
using namespace std;

const long INF = 1<<60;

class Edge{
public:
	int u,v,w;
	Edge(int u_, int v_, int w_): u(u_), v(v_), w(w_){
	
	}
};

void printPath(int t, vector<int>& p, vector<int>& d){
	if(d[t] == INF){
		cout << "No path" << endl;
		return;
	}

	if(p[t] == -1){
		cout << t << "->";
	}else{
		printPath(p[t], p, d);
		cout << t << "->";
	}

}


void bellman_ford(vector<Edge>& edges, int s, vector<int>& p, int n){

	/* normal implementation */
	vector<long> d(n, INF);
	d[s] = 0;
	int it=0;
	int last_vertex_relaxed = -1;
	
	for(int i=0;i<n;i++){
		last_vertex_relaxed = =-1;
		for(auto edge: edges){
			int u = edge.u;
			int v = edge.v;
			int w = edge.w;
			if(d[v] > d[u] + w){
				d[v] = max(-INF, d[u] + w);
				p[v] = u;
				last_vertex_relaxed = v;
			}
		}
		it = i+1;
		if(last_vertex_relaxed == -1){
			break;
		}
	}
	if(last_edge_relaxed == -1){
		// does not contain negative cycle
		/* print distances */
		for(int i=0;i<n;i++){
			cout << "Distance from node: " << s << " to node: " << i << " = " << d[i] << endl;
		}

		/* print path */
		for(int i=0;i<n;i++){
			printPath(i, d, p);
		}
		
	}else{
		// check for negative cycle
		if(has_cycle){
			int y = last_vertex_relaxed;
			for(int i=0;i<n;i++){
				y = p[y];
			}
			vector<int> cycle_path;
			for(int i=y; ; y = p[y]){
				cycle_path.push_back();
				if(i == y && cycle_path.size()>1){
					break;
				}
			}
		}
	}

}

int main(){
	int e; cin >> e;
	int n; cin >> n;
	vector<Edge> edges;
	for(int i=0;i<e;i++){
		int u,v,w;
		cin >> u >> v >> w;
		Edge e(u,v,w);
		edges.push_back(e);
	}

	int s; cin >> s;
	vector<int> p(n, -1);
	bellman_ford(edges, s, p, n);
	
}
```