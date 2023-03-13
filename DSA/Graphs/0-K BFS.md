> related to: [[BFS]], [[Graphs]]

> video: [riddi-dutta-youtube](https://www.youtube.com/watch?v=0hyTktYQ7WA) 

> reading: [cp-algorithms](https://cp-algorithms.com/graph/01_bfs.html), [codeforces-tutorial](https://codeforces.com/blog/entry/88408)

> practice: [Lame King](https://codeforces.com/contest/1804/problem/A)


## Table of Contents

- [0-1 BFS](#0-1%20BFS)
- [0-K BFS](#0-K%20BFS)

## 0-1 BFS

> BFS can be used to find shortest paths when all the edges have equal weights. Can we extend this? i.e., can we find shortest paths when the edges have weights (0,1) and the answer is yes.

- The idea is for all the adjacent vertices of current node `u`, if the adjacent vertex `v` is at distance 0, it basically means `u` and `v` are at the same level (if you think of vertices having levels) so push this vertex `v` at the front of the queue.
- If the adjacent vertex `v` is at distance 1, push at the back of the queue.
- the node is considered processed or visited when we pop it from the queue.
- Have additional checks to ensure we dont process the same node twice.

## 0-K BFS

- Similarly For short 'K' we can maintain k queues in a  vector
- For each adjacent vertex `v` of `u` we push it to a queue at `k_` distance **cyclically** if `k_` is edge weight.
- `q[(i+k_)%k].push(v)`
- once a queue is empty we  move to the next queue in the vector as long as there are nodes in any of the queues.