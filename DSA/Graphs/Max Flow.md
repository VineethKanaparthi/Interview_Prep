> related to: [[Graphs]], [[BFS]]
> reading: [cp-algorthms](https://cp-algorithms.com/graph/edmonds_karp.html), [usaco-guide](https://usaco.guide/adv/max-flow?lang=cpp), [[CPH.pdf|CPH-Page-191]] 

## Table of Contents

- [Focus Problems](#Focus%20Problems)
- [Maximum Flow](#Maximum%20Flow)
- [Minimum Cut](#Minimum%20Cut)
- [Maximum Flow and Minimum Cut Relationship](#Maximum%20Flow%20and%20Minimum%20Cut)
- [[Max Flow#Ford-Fulkerson Method For Max Flow|Ford-Fulkerson for Max Flow]]
- [[Max Flow#Extending Ford Fulkerson for Minimum Cut|Extending Ford Fulkerson for Minimum Cut]]

## Focus Problems

- **Finding a maximum flow** What is the maximum amount of flow we can send from one node to another.
- **Finding a minimum cut** What is a minimum weight set of edges that separates two nodes of the graph.

Input: Directed Weighted Graph that contains two special nodes: *source* and *sink*
		 - *source* doesnt have incoming edges
		 - *sink* doesnt have outgoing edges

## Maximum Flow

- In the maximum flow problem our task is to send as much flow as possible from the source to the sink. 
- The weight of each edge is a capactity that restricts the flow that can go through the edge.
- At each intermediate node( nodes except the source and sink), the incoming flow and outgoing flow has to be equal

## Minimum Cut

- I the minimum cut problem our task is to remove a set od edges from the graph such that there will be no path from the source to sink after the removal and The total wieght of the removed edges must be minimum

## Maximum Flow and Minimum Cut

- Maximum Flow and minimum cut are always equally large. These concepts are two sides of the same coin.

## Ford-Fulkerson Method For Max Flow

- read [cp-algorthms](https://cp-algorithms.com/graph/edmonds_karp.html), [[CPH.pdf|CPH-page-192]]

## Edmand-Karp

> edmand karp algorithm is an implementation of Ford-Fulkerson method to find the augmenting paths using [[BFS]]

#### Conditons and Terminology

- `capacity` matrix used to store the capacity for every pair of vertices
- `flow` is the actual amount of flow through each edge. (non negative)
- `flow` through an edge should be always $<=$ `capcity` of that edge.
- for all nodes except source and sink `inflow == outflow`
- for source and sink `outflow_source == inflow_sink`
- `residual capacity` of an edge is defined as `capacity - flow`
- `reverse edge residual capacity` is defined as `capacity_re - flow_re`
- if `flow_edge = f` then `flow_reverse_edge = -f`
- `capacity_re = 0`

#### Steps

- Initialize the residual capacity matrix i.e., `capacity - flow` for each edge.
- Initially flow will be `0` for all edges so residual capacity of an edge is just the capacity of edge.
- Initialize the reverse edge residual capacity matrix to all zeros i.e., `capacity_re - flow_re`.
- Initally flow will be `0` in the reverse edge and since capacity of reverse edges is `0`.
- Initalize a parent array with all `-1` except for the source node for which we will use `-2`
- insert source in queue with capacity `INF`  i.e., `queue<pair<int,long>> q; q.push({s, INF})`


## Extending Ford Fulkerson for Minimum Cut

#### Steps

- After finding max-flow, Let $A$ be the set of nodes that can be reached from source using positive weight.
- Minimum Cut Consists of the edges of the original graph that start at some node A, end at some node outside A and whose capacity is fully used in the maximum flow.


## Implementation

```C++

#include<bits/stdc++.h>
using namespace std;

class Solution
{
    const int INF = 1e9;
public:
    int bfs(vector<int> g[],vector<vector<int>>& capacity, int s, int t, vector<int>& parent){
        parent.assign(parent.size(), -1);
        parent[s] = -2;
        queue<pair<int,int>> q;
        q.push({s, INF});
        while(!q.empty()){
            int u = q.front().first;
            int flow = q.front().second;
            q.pop();
            for(auto& v: g[u]){
                if(parent[v] == -1 && capacity[u][v]){
                    parent[v] = u;
                    int min_flow = min(flow, capacity[u][v]);
                    if(v == t){
                        return min_flow;
                    }
                    q.push({v, min_flow});
                }
            }
        }
        return 0;
    }
    
    void print(vector<int>& parent){
        for(auto& p: parent){
            cout << p << " ";
        }
        cout << endl;
    }

	// minimum cut
	void dfs(vector<int> g[],vector<vector<int>>& capacity, vector<int>& visited, vector<int>& component, int u){
		visited[u] = 1;
		component.push_back(u);
		for(auto&v : g[u]){
			if(!visited[v] && capacity[u][v]){
				dfs(g, capacity, visited, component, v);
			}
		}
	}
    int findMaxFlow(int N,int M,vector<vector<int>> Edges)
    {
        // code here
        int n = N;
        vector<vector<int>> capacity(n, vector<int>(n, 0));
        vector<int> adj[n];
        for(auto& edge: Edges){
            int u = --edge[0];
            int v = --edge[1];
            int w = edge[2];
            capacity[u][v]+= w;
            capacity[v][u]+= w;
            adj[u].push_back(v);
            adj[v].push_back(u);
        }
        
        int flow = 0;
        int new_flow;
        vector<int> parent(n);
        while(new_flow = bfs(adj, capacity, 0, n-1, parent)){
            flow+=new_flow;
            int v = n-1, u = parent[v];
            while(v >= 0 && u >= 0){
                capacity[u][v]-=new_flow;
                capacity[v][u]+=new_flow;
                v = u;
                u = parent[v];
            }
        }

		// minimum cut
		vector<int> component;
		vector<int> visited(n, 0);
		dfs(g, capacity, visited, component, 0);
	
		for(auto& u: component){
			for(auto& v: g[u]){
				if(!visited[v]){
					cout << u+1 << " " << v+1 << "\n";
				}
			}
		}
        
        return flow;
        
    }
};

int main()
{
    int t;
    cin>>t;
    while(t--){
        int i,j,N,M,u,v,w;
        int res;
        scanf("%d %d",&N,&M);
        vector<vector<int>> Edges; 
        for(i=0;i<M;i++)
        {
            scanf("%d %d %d",&u,&v,&w);
        	Edges.push_back({u,v,w});
    	}
        Solution obj;
        res = obj.findMaxFlow(N, M, Edges);
        cout<<res<<endl;
    }
    return 0;
}
```


