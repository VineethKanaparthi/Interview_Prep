> related to: [[Graphs]]
> reading: [usaco-guide](https://usaco.guide/silver/func-graphs?lang=cpp), [cph](https://usaco.guide/CPH.pdf#page=164)
> videos: [unacademy](https://www.youtube.com/watch?v=IOJpKCAKFHc) 
> problem: [cses-planet-queries](https://cses.fi/problemset/task/1750/) 

## Table of Contents

- [Summary](# Summary)
- [Code](#code)

## Summary

- A functional graph is a graph where each node has an outdegree of 1.
- Successor Graphs are also called *Functional Graphs* because there has to be a function that defines the behaviour of the edges. The input for the function is the node itself and output is a successor node.
- So for an edge $u->v$ , $succ(u)=v$ .
- We can also define $succ(u, k)$ such that it gives a node that we will reach after $k$ steps if we start at node $u$.
- We can solve the above problem with [[Binary Lifting]]
- Cycle Finding in functional graphs with [[Floyds Cycle Detection Algorithm]]

## code

```C++
#include<bits/stdc++.h>
using namespace std;



int main(){
	ios_base::sync_with_stdio(false);
	cin.tie(NULL);
	int n,q;
	cin >> n >> q;
	int m = 30;

	int st[n][m];
	for(int i=0;i<n;i++){
		cin >> st[i][0];
		st[i][0]--;
	}
	for(int j=1;j<m;j++){
		for(int i=0;i<n;i++){
			st[i][j] = st[ st[i][j-1] ][j-1]; 
		}
	}

	/*for(int i=0;i<n;i++){
		for(int j=0;j<m;j++){
			cout << st[i][j]+1 << " ";
		}
		cout << endl;
	}*/

	while(q--){
		int x,k;
		cin >> x >> k;
		int ans = x-1;
		for(int i=m-1;i>=0;i--){
			if(k & (1<<i)){
				ans = st[ans][i];
			}
		}
		cout << ans+1 << '\n';
	}
}
```