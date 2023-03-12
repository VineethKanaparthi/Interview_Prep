> related to: [[Graphs]], [[DAG]], [[DFS]]
> reading: [cp-handbook](https://usaco.guide/CPH.pdf#page=161), 

## Table of Contents

- [Summary](#Summary)
- [Counting the no of paths](#counting_no_of_paths)

## Summary
---
> If a directed graph is acyclic, we can apply dynamice programming.
---

**Questions that can be answered with DP on DAG**
- How many different paths are there?
- What is the shortest/longest path?
- What is the minimum maximum edges in a path?
- Which nodes can certainly appear in any path.

#### counting_no_of_paths

> read: [cp-handbook](https://usaco.guide/CPH.pdf#page=162)

```c++
#include<bits/stdc++.h>
using namespace std;


bool has_cycle = false;

void dfs(vector<vector<int>>& g, vector<int>& color, stack<int>& order, int u){
	color[u] = 1;
	for(auto& v: g[u]){
		if(!color[v]){
			dfs(g, color, order, v);
			if(has_cycle){
				break;
			}
		}else if(color[v]==1){
			has_cycle = true;
			break;
		}
	}
	order.push(u);
	color[u] = 2;
}


void topological_ordering(vector<vector<int>>& g, stack<int>& order, int n){

	vector<int> color(n, 0);
	for(int i=0;i<n;i++){
		if(!color[i]){
			dfs(g, color, order, i);
		}

	}

}

void find_no_paths(vector<vector<int>>& g, stack<int>& topological_order, vector<int>& paths){
	int n = topological_order.size();

	vector<vector<int>> g_t(n);
	for(int u=0;u<n;u++){
		for(auto& v: g[u]){
			g_t[v].push_back(u);
		}
	}

	while(!topological_order.empty()){
		int u = topological_order.top();
		topological_order.pop();
		if(g_t[u].size()==0){
			paths[u] = 1;
		}else{
			for(auto& v: g_t[u]){
				paths[u]+= paths[v];
			}

		}
	}


}

int main(){

	int n,m;
	cin >> n >> m;
	vector<vector<int>> g(n);
	for(int i=0;i<m;i++){
		int u,v;
		cin >> u >> v;
		u--;v--;
		g[u].push_back(v);
	}

	stack<int> topological_order;
	topological_ordering(g, topological_order, n);


	if(!has_cycle){
		vector<int> paths(n, 0);
		find_no_paths(g, topological_order, paths);

		for(int i=0;i<n;i++){
			cout << paths[i] << " ";
		}
		cout << endl;
	}

}
```




