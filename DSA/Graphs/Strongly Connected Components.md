> related to: [[Graphs]], [[DFS]]
> reading: [cp-algorithms-kosaraju](https://cp-algorithms.com/graph/strongly-connected-components.html), [top-coder-kosarajus](https://www.topcoder.com/thrive/articles/kosarajus-algorithm-for-strongly-connected-components) 

## Table of Contents

- [Summary](#Summary)
- [Kosaraju's Algorithm](#Kosarajus_Algorithm)

## Summary

- SSC's are a concept of Directed Graphs
---
> What are Strongly Connected Components?
---
- Strongly Connected Components are maximal subset of nodes in a directed graph where any two nodes in the subset can be reached from each other.
- What is a maximal subset? i.e., longest subset of nodes in the graph which holds the above property of reachability
- SCC's do not intersect each other i.e., they dont have any common vertices. If they do by definition both of them can be merged to a single SCC
---
> What is a Condensation Graph?
---
- Condensation graph is a graph where each node is a strongly connected component of the orginal graph
- Condensation graph is *acyclic* i.e., there are no cycles because if it does, all the nodes of all SCC's in the cycle can be reached from one another, so they can all be merged to a single SCC.
- Every edge in the condensation graph is called *oriented edge*

## Kosarajus_Algorithm

#### key-points
- **First DFS** Run a series of DFS and note down order of exit times.
- sort the nodes in decreasing order of exit times
- **Second DFS** on transposed graph. Maintain a component vector to collect the nodes in that strongly connected component. Make the first node as root of that component.
- Iterate through every node and its edges. if their roots are different add an edge between them.

```C++
#include <bits/stc++.h>
using namespace std;

void dfs1(vector<vector<int>>& g, vector<bool>& visited, vector<int>& order,  int u){
	visited[u] = true;
	for(auto& v: g[u]){
		if(!visited[v]){
			dfs1(g, visited, order, v);
		}
	}
	order.push_back(u);
}

void dfs2(vector<vector<int>>& g, vector<bool>& visited, vector<int>& component,  int u){
	visited[u] = true;
	component.push_back(u);
	for(auto& v: g[u]){
		if(!visited[v]){
			dfs1(g, visited, order, v);
		}
	}
}



int main(){
	int n,m; cin >> n >> m;
	vector<vector<int>> g(n),gt(n);
	for(int i=0;i<m;i++){
		int u,v;
		cin >> u >> v;
		g[u].push_back[v];
		gt[v].push_back[u];
	}

	// dfs1
	vector<bool> visited(n, false);
	vector<int> order;
	for(int i=0;i<n;i++){
		if(!visited[i]){
			dfs1(g, visited, order, i);
		}
	}

	reverse(order.begin(), order.end());
	
	//dfs2
	visited.assign(n, false);
	vector<int> component;
	vector<int> roots;
	vector<int> root;
	for(auto& v: order){
		if(!visited[v]){
			dfs2(gt, visited, component, v);
			int r = component[0];
			roots.push_back(r);
			for(auto& u: component){
				root[u] = r;
			}
			component.clear();
		}
	}

	vector<vector<int>> adj_scc(roots.size());
	for(int u=0;u<n;u++){
		for(auto& v: g[u]){
			int root_u = root[u], root_v = root[v];
			if(root_u != root_v){
				adj_scc[root_u].push_back(root_v);
			}
		}
	}

}
```