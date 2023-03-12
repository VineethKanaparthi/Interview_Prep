> Implementation: [algo tree](https://www.algotree.org/algorithms/single_source_shortest_path/dijkstras_shortest_path_c++/) , [cp-algorithms-pq-implementation](https://cp-algorithms.com/graph/dijkstra_sparse.html#priority_queue) , [cp-algorithms-set-implementation](https://cp-algorithms.com/graph/dijkstra_sparse.html#set)
> Related to [[Prims]],  [[DFS]], [[Bellman-Ford]], [[Floyd-Warshall]]
> reading: [usaco-guide](https://usaco.guide/gold/shortest-paths?lang=cpp#dijkstra), [cp-algorithms](https://cp-algorithms.com/graph/dijkstra.html)
> Read usaco-guide carefully

## Table-of-Contents

- [Key Points](#Key-Points)
- [Implementation](#Implementation)
- [Complexity Analysis](#Complexity-Analysis)
- [Variation](#Variation)
- [Generating a shortest path DAG from Dijkstras](#Dijkstras-DAG)

## Key-Points
- Dijkstra's is a Single Source Shortest Path Algorithm
- Dijkstra’s algorithm finds the shortest path in a *weighted graph*  containing *only positive edge* weights from a single source.
- In some cases it *may find* shortest path in graphs containing *negative edges* as well
- Since [[Dijkstra's]] doesnt work on graph with negative weight edges, [[Bellman-Ford]] is used in such cases.
- Main concepts used are *priority_queue* and *edge-relaxation* 

## Implementation

```c++
/*
* Implementation of Dijkstra's single source shortest path algoirthm using
* adjacency list data structure on a weighted undirected graph. 
*/

#include <bits/stcc++.h>
use namespace std;

const int INF = INT_MAX;

void getPath(int v, vector<int>& distance, vector<int>& parent){
	if(distance == INF){
		cout << "No path";
		return;
	}
	if(parent[i] == -1){
		cout << i << " -> ";
		return;
	}
	getPath(parent[i], distance, parent);
	cout << i  << " -> ";
}

int main(){
	int n; cin >> n;
	
	/* construct graph from edges */
	
	vector<vector<pair<int,int>>> g(n);
	int e; cin >> e;
	int u,v,w;
	for(int i=0;i<e;i++){
		cin >> u >> v >> w;
		g[u].push_back({v,w});
		g[v].push_back({u,w});
	}
	
	/* Dijkstras on adj list */
	
	int source; cin >> source; 
	vector<int> distance(n, INF);
	vector<int> parent(n, -1);
	distance[source] = 0;
	priority_queue<pair<int,int>> pq;
	pq.push(0, source);
	parent[source] = -1;
	
	while(!pq.empty()){
		int dis = pq.top().first;
		int node = pq.top().second;
		pq.pop();
		/* 
		* This check is important because, there might be several pairs of 
		* the same vertex. We only need the latest pair which has the minimum 
		* distance to this vertex. Hence we do the following check. Log(E)
		*  
		* In Other Languages we first erase existing pair and then push a new 
		* pair. log(V). Alternatively we can use set in C++.
		* 
		* 
		*/
		if (dis != distance[node]) {
			continue;
		}
		for(auto edge : g[node]){
			int adj_node = edge.first;
			int edge_weight = edge.second;
			if(distance[adj_node] > dis + edge_weight){
				distance[adj_node] = dis + edge_weight
				parent[adj_node] = node;
				pq.push({distance[adj_node], adj_node});
			}	
		}
	}

	/* print distances */
	
	for(int i=0; i<n; i++){
		cout << "Source Node(" << source << ") -> Destination Node(" << i << ") : " << distance[i] << endl; 
	}

	/* print paths */
	
	for(int i=0;i<n;i++){
		getPath(i, distance, parent);
		cout << endl;
	}
	
}
```

## Complexity-Analysis
- Total no of edges in pq in worst case is E i.e., no of edges
- So extracting min in pq is  `log(E)` and we do it `E` times in worst case.
- Once we extract min, it means for that node by now we have the shortest path.
- We only go to the second loop V times  because of the check we are doing and each Edge of each vertex will be parsed only once in the process of relaxation. So, The second operation will run for a max of E times which is $\sum_{i=0}^{V} E_i$ . (V * E<sub>i</sub> i.e., equals 2 * E)
- so the complexity with priority queue is `(E*Log(E) + 2*E)` which reduces to `O(E*log(E))`

## Variation

> If we want min distance from a set of source nodes we can do the following modification to the below algorithm.
> Example: Given a DAG with a set of nodes, some of which are hospitals, find the nearest hospital from each node. 
> Sol: Reverse the DAG and apply dijkstras with all the hospitals as sources.

```c++
for(auto source : sources){
	pq.push({0, source})
}
```

## Dijkstras-DAG

> reading: [cp-handbook](https://usaco.guide/CPH.pdf#page=163) 

```C++
	vector<vector<int>> dag(n), dag_rev(n);
	for(int u=0;u<n;u++){
		for(auto& edge: g[u]){
			int v = edge.first;
			int w = edge.second;
			if(distance[u]+w == distance[v]){
				dag[u].push_back(v);
				dag_rev[v].push_back(u);
			}
		}
	}
```

- [Back to top](#Table-of-Contents)
