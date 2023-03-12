> Related to : [[Graphs]], [[DFS]]
> reading: [cp-algorithms](https://cp-algorithms.com/graph/bridge-searching.html)
> videos: [codencode](https://www.youtube.com/watch?v=LNc4BqhDsPw&list=PL5DyztRVgtRVLwNWS7Rpp4qzVVHJalt22&index=22)


## To-Do
- [ ] read https://codeforces.com/blog/entry/68138 when you have time
---
## Table of Contents

- [Summary](#Summary)
- [Algorithm](#Algorithm)
- [Implementation](#Implementation)

---
## Summary
----
> What is a bridge?
---
- In a graph, a bridge is an edge which when removed increases the no of connected components in that graph. (Red edges in the below graph)

-                                                        ![[bridges-example.png|150]]
- The *problem* can be thought of as, given a map of cities connected with roads, find all the important roads i.e., without those roads the connectivity gets disrupted
---
## Algorithm
---
- [[DFS]] can be used here with some modifications
- **Main idea** is that,  an edge $(u, v)$ is a bridge only if there is no other path from $u$ to $v$ except the edge $(u, v)$
- How to check for this?
- We can use the *time of entry to node* computed by *dfs*
- We can maintain an array `time_in` which will have entry time for each node and an array `low_a` which will have lowest ancestor $v$ can reach through a back edge.
- `low_a[v] = min(time_in[v], min(time_in[p]), low[x])`
- where $p$ is node to which v has a back-edge. (what is a back edge, in dfs we reach a node that is already visited - it is a back edge.) 
- $x$ is all nodes which are direct descendants of $v$ in dfs tree.
---
## Implementation
---

```C++
#include <bits/stdc++.h>
using namespace std;
int time = 0;

void dfs(vector<vector<int>>& g, vector<bool>& visited, vector<int>& in_time, vector<int>& low_a, int v, int p){
	visited[v] = true;
	in_time[v] = low_a = time++;
	for(auto u : g[v]){
		if(u == p){
			// we only want to check back edges that are u->v
			continue;
		}
		if(visited[u]){
			low_a[v] = min(low_a[v], in_time[u]);
		}else{
			dfs(g, visited, in_time, low_a, u, v);
			low_a[v] = min(low_a[v], low_a[u]);
			if(low_a[u] > in_time[v]){
				// u->v  is a bridge
			}
		}
	}
}

int main(){
	int n; cin >> n;
	int e; cin >> e;
	vector<vector<int>> g(n);
	for(int i=0;i<e;i++){
		int u,v;
		cin >> u >> v;
		g[u].push_back[v];
		g[v].push_back[u]; // if undirected graph
	}

	vector<bool> visited(n, false);
	vector<int> in_time(n, 0);
	vector<int> low_a(n);
	dfs(g, visited, in_time, low_a, 0, -1);
}
```