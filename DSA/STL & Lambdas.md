> Related to: [[DSA Prep]], [[Strings]]

## Table of Contents

- [[STL & Lambdas#Vectors | Vector]]
- [[STL & Lambdas#Strings | Strings]]

## Lambda

> reading: [umich-pdf](http://websites.umich.edu/~eecs381/handouts/Lambda.pdf) 

**Basic Syntax**
	`[capture list](parameter list){function body}(actual parameters)`

specifying return type: `[](parameter list)->return_type{};`

`[&]` -> `&` in capture list means, the lambda has access to all the variables in the scope where lambda is declared.

- [ = ] capture all variables currently in local block scope by copy of their current values 
- [ & ] capture all variables currently in local block scope by reference


## Vectors
	- v(n, 0)
	- v(a.begin(), a.end())
	- v(arr, arr+5)
	- v(arr+1, arr+4)
	- v(v.begin()+1, v.end())
	- v.insert(v.begin(), 100) // inserts 100 at 0th index
	- v.insert(v.begin()+1, 100)
	- v.emplace_back()
	- v.emplace(v.begin(), 100) // similar to insert
	- v.front()
	- v.back()

## Strings
	- str.swap(another_str)


## Tuples

```C++
tuple<int,int,int> t{3,4,5};
get<1>(t); // returns 4
tie(a,b,c) = t; // will assign 3 4 5 to a,b,c respectively

// we can also do the following 

tuple<int,int,int> t = tie(a,b,c); // to assign a bc to a tuple
```

