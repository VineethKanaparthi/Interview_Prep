> related to [[Graphs]], [[BFS]], [[DFS]], [[Connected Components]]
> videos: [codencode playlist](https://www.youtube.com/playlist?list=PL5DyztRVgtRVLwNWS7Rpp4qzVVHJalt22)
----
> Types of Problems
------
- [DFS on 2D Grid](#DFS)
- [BFS on 2D Grid](#BFS)
- [Counting Connected Components in 2D Grid](#Connected-Components)
----
### DFS
---
> Example problem: Given a starting point and an ending point, find the minimum no of moves required to reach the ending point from starting point (or) count the total number of ways. Later can be solved with DP as well (but only can move right or down).
> problem: [jungle-run](https://www.hackerearth.com/practice/algorithms/graphs/depth-first-search/practice-problems/algorithm/jungle-run/) 

#### Key points in implementation

- Checking if the next direction is a valid direction to go to via `isValid(i,j,n)`
- Checking if the next point is not yet visited through a `visited == true` grid
- Checking if the next point can be traveresed through `grid[i][j] == some_value`
---
### BFS
---
> Time/Level based problems. Example. Given a grid with 0,1,2. In each unit of time all the 1's adjacent to 2 will be flipped to 2. Find the time in which the operations ripple stops or minimum time in which all the 1's will be converted to 2's

#### Key points in implementation

- Maintain a queue, push the start vertex and mark it as visited
- While queue is not empty repeat
	- top and pop
	- visit their adjacent edges if they are `valid && !visited && a path exists`
	- mark them as visited
	- push them to queue



---
### Connected-Components
> problems: [counting-rooms](https://cses.fi/problemset/task/1192/) 

#### Key points in implementation

- Run DFS/BFS multiple times as long as there are valid cells to be visited
```C++
for(int i=0;i<n;i++){
	for(int j=0;j<m;j++){
		if(isValid(i,j,n,m) && grid[i][j] && !visited[i][j]){
			dfs(grid, visited, n, m, {i,j});count++;
		}
	}
}
```



