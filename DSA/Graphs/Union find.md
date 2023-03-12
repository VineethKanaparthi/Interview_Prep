> related to: [[Graphs]]
> reading: [usaco](https://usaco.guide/gold/dsu?lang=cpp) [leet-code-graphs](https://leetcode.com/explore/learn/card/graph/618/disjoint-set/)
> videos: [cf-itmo-course](https://codeforces.com/edu/course/2/lesson/7) 

## Table of Contents

- [To-Do](#To-Do)
- [Code](#code)

## To-Do

- [ ] read usaco and cf material

## code

```C++
#include<bits/stdc++.h>
using namespace std;
 

class UnionFind{
	int n;
	vector<int> root;
	vector<int> rank;
	vector<int> size;
public:
	int cc;
	int max_size;
	UnionFind(int n_): n(n_),cc(n_),rank(n,1), max_size(1), root(n), size(n,1){
		for(int i=0;i<n;i++){
			root[i] = i;
		}
	}

	int find(int u){
		if(u == root[u]){
			return u;
		}
		return root[u] = find(root[u]);
	}

	void add(int u, int v){
		int root_u = find(u);
		int root_v = find(v);
 		if(root_u != root_v){
			if(rank[root_u] > rank[root_v]){
				root[root_v] = root_u;
				size[root_u]+=size[root_v];
				size[root_v]=0;
				max_size = max(max_size, size[root_u]);
			}else if(rank[root_u] < rank[root_v]){
				root[root_u] = root_v;
				size[root_v]+=size[root_u];
				size[root_u]=0;
				max_size = max(max_size, size[root_v]);
			}else{
				root[root_v] = root_u;
				rank[root_u]++;
				size[root_u]+=size[root_v];
				max_size = max(max_size, size[root_u]);
			}
			cc--;
		}
	}
};

int main(){
	ios_base::sync_with_stdio(false);
	cin.tie(NULL);
	int n,m;
	cin >> n >> m;
	UnionFind uf(n);
	for(int i=0;i<m;i++){
		int u,v; cin >> u >> v;
		u--;v--;
		uf.add(u,v);
		cout << uf.cc << " " << uf.max_size << "\n";
	}



	
}
```