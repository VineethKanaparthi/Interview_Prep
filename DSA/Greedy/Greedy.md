> related to: [[DSA Prep]], [[Exchange Arguments]]
> videos: [algorithms-live](https://www.youtube.com/watch?v=Oq1seKJvfQU) 
> read: [[Exchange Arguments]], [greedy is good from topcoder](https://www.topcoder.com/thrive/articles/Greedy%20is%20Good) 
> read: [Greedy Slides From Stanford CS161](https://web.stanford.edu/class/archive/cs/cs161/cs161.1138/), [Handout from Stanford CS161](https://web.stanford.edu/class/archive/cs/cs161/cs161.1138/handouts/120%20Guide%20to%20Greedy%20Algorithms.pdf)

## Table of Contents

- [To-Do](#To-Do)
- [[Greedy#Summary|Summary]]
- [[Greedy#How to prove that greedy works]]
- [[Greedy#Foot Notes | Points to Keep in Mind]]

## To-Do

> read [UW Madison CS Greedy handout](https://pages.cs.wisc.edu/~dieter/Courses/2004F-CS787/Scribes/greed.pdf) ,[ williams cs greedy guide](http://cs.williams.edu/~shikha/teaching/spring20/cs256/handouts/Guide_to_Greedy_Algorithms.pdf) 

## Summary

> Greedy Algorithms construct the globally best option/solution by repeatedly choosing the locally best option

- Greedy Algorithms are *Simple* and *Efficient* but *Hard to design* and *Hard to verify*

## How to prove that greedy works

> reading: stanford cs 161 handout and ppt


### Method 1: Greedy Stays Ahead

- *Lemma 1*: First Prove that greedy finds *A* Solution
- *Lemma 2*: Prove that Greedy is the optimal 

General Steps:
- Find a series of measurements $M_{1},M_{2},....M_{k}$ you can apply to any solution
- Show that greedy algorithm's measures are atleast as good as any solutions measure
- Prove that because the greedy solution's measures are atleast as good as any solution, the greedy solution must be optimal.

### Method 2: Exchange Arguments

- watch Algorithms Live Exchange Arguments video


## Foot Notes

- a problem that seems extremely complicated on the surface (see [TCSocks](http://www.topcoder.com/stat?c=problem_statement&pm=2894&rd=5853)) might signal a greedy approach. 
- problems with a very large input size (such that a n^2 algorithm is not fast enough) are also more likely to be solved by greedy than by backtracking or [dynamic programming](http://www.topcoder.com/tc?module=Static&d1=tutorials&d2=dynProg).
- despite the rigor behind them, you should look to the greedy approaches through the eyes of a detective, not with the glasses of a mathematician.
- in addition, study some of the standard greedy algorithms to grasp the concept better ([Fractional Knapsack Problem](http://www-cse.uta.edu/~holder/courses/cse2320/lectures/l15/node3.html), [Prim Algorithm](http://www-b2.is.tokushima-u.ac.jp/~ikeda/suuri/dijkstra/Prim.shtml), [Kruskal Algorithm](http://www-b2.is.tokushima-u.ac.jp/~ikeda/suuri/kruskal/Kruskal.shtml), [Dijkstra Algorithm](http://www-b2.is.tokushima-u.ac.jp/~ikeda/suuri/dijkstra/Dijkstra.shtml), [Huffman Coding](http://www.cs.duke.edu/csed/poop/huff/info/torials&d2=index), [Optimal Merging](http://www.maths.abdn.ac.uk/~igc/tch/mx4002/notes/node45.html), [Topological Sort](http://www.owlnet.rice.edu/~comp314/04spring/lec/week6/Topological.htm)).

