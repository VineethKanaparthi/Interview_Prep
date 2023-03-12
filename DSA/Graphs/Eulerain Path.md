> related to: [[Graphs]], [[DFS]], [[Hamiltonian Path]]
> reading: [usaco-guide](https://usaco.guide/adv/eulerian-tours?lang=cpp), [cp-algorithms](https://cp-algorithms.com/graph/euler_path.html)
> video: [WilliamFiset-eulerian-path-existence](https://www.youtube.com/watch?v=xR4sGgwtR2I&list=PLDV1Zeh2NRsDGO4--qE8yH72HFL1Km93P&index=27), [WilliamFiset-Algorithm](https://www.youtube.com/watch?v=8MpoO2zA2l4&list=PLDV1Zeh2NRsDGO4--qE8yH72HFL1Km93P&index=28), [WilliamFiset-Code](https://www.youtube.com/watch?v=8MpoO2zA2l4&list=PLDV1Zeh2NRsDGO4--qE8yH72HFL1Km93P&index=28) 
> Note: Watch the videos first

## Table of Contents

- [Summary](#Summary)
- [Existence Check](#Existence%20Check)
- [Algorithm](#Algorithm)
- [code for undirected graph](#code%20for%20undirected%20graph)

## Summary

- A **Eulerian Path** is a path in a graph that goes through each edge exactly once.
- A **Eulerian Circuit** is a **Eulerian Path** that starts and ends at the same node.

## Existence Check

- The existence of eulerian paths and circuits depends on the degrees of nodes.
-  An undirected graph has a eulerian path if
	- All the nodes belong to the same connected component
	- The degree of nodes are all even (**Eulerian Circuit**) or all are even except 2 nodes(starting and ending node)
- A directed graph has a eulerian path
	- If all the nodes belong to the same connected component
	- In each node, the indegree == outdegree (*or*)
	- In one node, indegree = outdegree+1 and another node outdegree = indegree+1 and all other nodes have indegree == outdegree

## Algorithm

#### Heirholtzer's Algorithm

> Modify if undirected
- Verify the existence by comparing the degrees.
- Verify that its stronly connected and the nodes that are unvisited are the ones with 0 out and indegree.
- Finding a starting node:
	- Start with a node which has outdegree > indegree, if there is no such node you can start with any node.
	- Ends at a node which has indegree > outdegree, if there is no such node you end at where you start
- Apply modified DFS:
	- As long as there are outgoing edges to visit: (hint: out degree)
		- apply dfs on the outgoing edges
	- After visiting all the outgoing edges, add node to stack



#### code for undirected graph

> problem: [cses-mail-delivery](https://cses.fi/problemset/task/1691/)

```C++
#include<bits/stdc++.h>
using namespace std;
 

class Edge{
public:
	int u,v,revi;
	Edge(int u, int v, int revi):u(u), v(v),  revi(revi){}
};


void dfs(vector<Edge> g[], stack<int>& order, int u){
	while(!g[u].empty()){
		Edge e = g[u].back();
		g[u].pop_back();
		if(e.v != -1){
			g[e.v][e.revi].v = -1;
			dfs(g, order, e.v);
		}
	}
	order.push(u);
}

int main(){
	// diables syncronisation between C and C++ streams. So use only C IO or C++ IO
	ios_base::sync_with_stdio(false);
	// unties cin and cout. If the streams are tied, one is flushed before executing IO operation on another
	cin.tie(NULL);

	int n,m; cin >> n >> m;
	vector<Edge> g[n];
	vector<int> degree(n, 0);

	for(int i=0;i<m;i++){
		int u,v;
		cin >> u >> v;
		u--;v--;
		degree[u]++; degree[v]++;
		g[u].push_back({u, v, (int)g[v].size()});
		g[v].push_back({v, u, (int)g[u].size()-1});
	}

	int even_degree=0, odd_degree = 0, int start_node = -1;
	for(int i=0;i<n;i++){
		if(degree[i]){
			if(degree[i]%2){
				odd_degree++;
				start_node = i;
			}else{
				even_degree++;
				if(start_node == -1){
					start_node = i;
				}
			}
		}
	}

	if(!odd_degree || !even_degree){
			start_node = 0;
	}

	stack<int> order;
	if(odd_degree == 0 || odd_degree == 2){
		dfs(g, order, start_node);
	}

	if((int)order.size() == m+1){
		while(!order.empty()){
			cout << order.top()+1 << " "; order.pop();
		}
	}else{
		cout << "IMPOSSIBLE" << endl;
	}
}
```


#### code for undirected graph

```C++
#include<bits/stdc++.h>
using namespace std;
 

void dfs(vector<int> g[], vector<int>& outdegree, stack<int>& order, int u){
	while(outdegree[u]){
		dfs(g, outdegree, order, g[u][--outdegree[u]]);
	}
	order.push(u);
}


int main(){
	// diables syncronisation between C and C++ streams. So use only C IO or C++ IO
	ios_base::sync_with_stdio(false);
	// unties cin and cout. If the streams are tied, one is flushed before executing IO operation on another
	cin.tie(NULL);

	int n,m; cin >> n >> m;
	vector<int> indegree(n,0),outdegree(n,0);
	vector<int> g[n];
	for(int i=0;i<m;i++){
		int u,v;
		cin >> u >> v;
		u--;v--;
		g[u].push_back(v);
		outdegree[u]++;
		indegree[v]++;
	}

	int out=0,in=0, start_node = -1;
	for(int i=0;i<n;i++){
		if(outdegree[i] == indegree[i]){
			continue;
		}else if(outdegree[i]-indegree[i] == 1){
			start_node = i;
			out++;
		}else if(indegree[i]-outdegree[i] == 1){
			in++;
		}else{
			start_node = -1;
			break;
		}

		if(start_node == -1 && outdegree[i]){
			start_node = i;
		}
	}

	stack<int> order;
	if(start_node!=-1 && ((out==1 && in ==1) || (out==0 && in==0) )) {
		dfs(g, outdegree, order, start_node);
	}


	if(order.size() == m+1){
		while(!order.empty()){
			cout << order.top()+1 << " "; order.pop();
		}	
	}else{
		cout << "IMPOSSIBLE" << endl;
	}


	return 0;
	
}
```