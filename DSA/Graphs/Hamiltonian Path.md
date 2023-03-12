> related to: [[Graphs]], [[Eulerain Path]]
> reading: [cp-handbook](https://usaco.guide/CPH.pdf#page=183)
> video: [fit-coder](https://www.youtube.com/watch?v=jGRRBJlNtwI&list=PLFj4kIJmwGu0yzwN3qZmw6p3E3zpoHpZz&index=14)
> bitmask-dp: [usaco-guide](https://usaco.guide/gold/dp-bitmasks?lang=cpp#bitmask-dp)



## Table of Contents

- [Summary](#Summary)

## Summary

- A Hamiltonian Path is a path that visits each node exactly once.
- Checking existence of hamiltonian path is a NP-Hard Problem and no efficient algorithm is known for solving the problem
- Use DFS + backtracking


```C++
#include<bits/stdc++.h>

using namespace std;

int cnt=0;

int m = 1e9+7;

void dfs(vector<int> g[], vector<bool>& visited, int n, int u, int pathc){

	visited[u] = true; pathc++;
	
	//cout << u << ":" << pathc << ":" << cnt << endl;
	
	if(u == n-1 && pathc == n){
	
		cnt = (cnt%m + 1%m)%m;
	
	}

	if(u!=n-1){
	
		for(auto& v: g[u]){
		
			if(!visited[v]){
			
				dfs(g, visited, n, v, pathc);
			
			}
	
		}

	}

	visited[u] = false;

}

int main(){

	// diables syncronisation between C and C++ streams. So use only C IO or C++ IO
	
	ios_base::sync_with_stdio(false);
	
	// unties cin and cout. If the streams are tied, one is flushed before executing IO operation on another
	
	cin.tie(NULL);
	
	int n,m;
	
	cin >> n >> m;
	
	vector<int> g[n];
	
	for(int i=0;i<m;i++){
	
		int u,v;
		
		cin >> u >> v;
		
		u--;v--;
		
		g[u].push_back(v);
	
	}
	
	vector<bool> visited(n, false);
	
	dfs(g, visited, n, 0, 0);
	
	cout << cnt << endl;

}
```
