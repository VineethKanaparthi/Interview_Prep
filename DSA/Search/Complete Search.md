> related to: [[Recursion]]
> reading:  [[CPH.pdf|CPH Page 57]]

## Table of Contents

- [[Complete Search#Generating Subsets|Generating Substes]]
- [[Complete Search#Generating Subsets using recursion|Generating subsets using recursion]]
- [[Complete Search#Generating subsets using bitmask|Generating subsets using bitmask]]

## Generating Subsets

> problem: Generate subset of n elements
> Ex: {0,1,2} ->  null, {0}, {1}, {2}, {0,1}, {0,2}, {1,2}, {1,2,3}
> idea:
> Include the current element and generate
> dont include the current element and generate
> Continue to do this for all elements

- For n elements there are $2^n$ subsets.
- We can generate and check for all subsets if n<=20
- We can generate subsets in 2 ways
	- Recursive
	- Bitmask

## Generating Permutations

> Permutation: A permutation is a reordering of a list of elements
> idea: maintain a kind of visited array or used array, Visualise how the recursion works. What all calls will we making in the first step, second step so on and when do we terminate.
> For permutation we go on further if we decide to include atleast something

```C++
void generatePermuatation(string& s, string permutation, vector<int>& used){
	if(permuation.size() == s.size()){
		cout << permutation << "\n";
	}else{
		for(int i=0;i<n;i++){
			if(!used[i]){
				used[i]=true;
				generatePermutation(s, permutation, used);
				used[i]=false;
			}
		}
	}
}
```

## Generating Subsets using recursion

```C++
vector<vector<int>> subsets;

void generate(int i, vector<int>& elements, vector<int>& subset){
	if(i == elements.size()){
		subsets.push_back(subset);
	}else{
		generate(i+1, elements, subset);
		subset.push_back(elements[i]);
		generate(i+1, elements, subset);
		subset.pop_back();
	}
}
```

## Generating subsets using bitmask

```C++
void generate(vector<int>& elements){
	int n = elements.size();
	for(int i=0;i<(1<<n);i++){
		vector<int> subset;
		for(int j=0;j<n;j++){
			if(i&(1<<j)){
				subset.push_back(elements[j]);
			}
		}
		subsets.push_back(subset);
	}
}
```

