> related to: [[Greedy]]


## Technique of Probing:
> Think about what properties the optimal solution will have

- probe it for optimal solutions

#### Example: Proving that we will always get optimal solution to make change using the US coin denomination

- Probe it for optimal solution
- Suppose the optimal solution has 3 dimes
	- We can always replace it with 1 quarter and 1 nickel
	- So we can have atmost 2 dimes
- Suppose the optimal solution has 2 nickels
	- We can replace it with 1 dime
	- So we can have atmost 1 nickel
- Suppose the optimal solution has 5 pennies
	- We can replace it with 1 nickel
	- We can have at most 4 pennies
- Also, we cant have both 2 dimes and 1 nickel at the same time
	- We can replace them with 1 quarter
- Anything that is not quarter, 
	- sum of all those coins will be 24 at max
- Samething goes for dimes, atmost 9
- Samthing for nickels, atmost 4


#### Proof of Greedy for US Coin Change

- let $O^*$ be our optimal solution and $G$ be greedy solution.
- Let $q$ qnd $q^`$ be no of quarters in $O^*$ and $G$ respectively
- Optimal solution will never have more coins of quarters than Greedy solution.
- So either $q=q^`$ or $q<q^`$
- If the optimal solution has less quarters, this cant be because we can always replace the dimes and nickels with quarters i.e.,  we cant replace quarters with nickels and dimes. (see: Probing)
- same with dimes
- same with nickels
- if the all of the other coins are same in $O^*$ and $G$ , nickels will also be same
- So $O^*$ = $G$, which also tells us that it is unqiue

#### Rough For TheProgrammingContestDivOne Problem

We have a greedy solution
We have a optimal solution

Probing:

We have reward, decay per second and time it takes to solve
We have to probelms with $r_{i}, d_{i}, t_{i}$  and  $r_{j}, d_{j}, t_{j}$ 
How do we choose

Two ways to choose

1)  $r_{i}-d_{i}*t_{i} + r_{j} - d_{j}*(t_{i}+t_{j})$
2) $r_{j}-d_{j}*t_{j} + r_{i} - d_{i}*(t_{i}+t_{j})$
3) So if we want choose i first $r_{i}-d_{i}*t_{i} + r_{j} - d_{j}*(t_{i}+t_{j})>=r_{j}-d_{j}*t_{j} + r_{i} - d_{i}*(t_{i}+t_{j})$
4) Simplifying $-d_{i}*t_{i}  - d_{j}*(t_{i}+t_{j})>=-d_{j}*t_{j}  - d_{i}*(t_{i}+t_{j})$
5) further Simplifying: $-d_{i}*t_{i}  - d_{j}*t_{i}-d_{j}*t_{j}>=-d_{j}*t_{j}  - d_{i}*t_{i}-d_{i}*t_{j}$
6) Simplifying $- d_{j}*t_{i}>=-d_{i}*t_{j}$
7)  $d_{j}*t_{i}<=d_{i}*t_{j}$
8) $t_{i}/t_{j}<=d_{i}/d_{j}$
