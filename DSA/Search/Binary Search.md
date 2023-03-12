> related to: [[DSA Prep]]
> reading: [usaco](https://usaco.guide/silver/binary-search?lang=cpp) , [cp-algorithms](https://cp-algorithms.com/num_methods/binary_search.html) 
> videos: [itmo-cf](https://codeforces.com/edu/course/2/lesson/6), [priyansh-agarwal](https://www.youtube.com/watch?v=TiQ_W2qG3kU)
> notes: watch the itmo-cf and do the practice questions

## To-Do

- [ ] Codeforces Edu Step 4
- [ ] Codeforces Edu Step 5
- [ ] Ternary Search (from cp algorithms)
- [ ] [parallel binary search](https://codeforces.com/blog/entry/45578)

## Table of Contents

- [[Binary Search#Important Notes | Must Read Important Notes]]
- [[Binary Search#Binary Search on Real Numbers | Binary Search on real numbers]]
- [[Binary Search#Traditional Implementation | Traditional Question]]
- [[Binary Search#Alternative Implementation | Traditional Question Alternative Implementation]] 
- [[Binary Search#First Element Implementation | Find the first element that matches]]
- [[Binary Search#Last Element Implementation | last element that matches]]

## Important Notes

- How to find a good `r` value? 
- Find a power of 2 which satisfies or doesn't the condition i.e.,
```C++
long long r = 1;
while(!f(x)){
	r*=2;
}
```
- Types of problems:
	- Application on monotonic functions
	- Binary search on answer. (Ex: Maximise or Minimise something)
	- Minimize the maximum or Maximise the minimum
	- Maximise or Minimize a Function on a set of segments or sets
	- Find the Kth element

## Binary Search on Real Numbers

> Be Mindful of three key points
> set good $l$ and $r$ values depending on the precision they are expecting, generally 0 and some large integer r will be good. 
> when to terminate? when abs(r-l) <= precision so continue `while(abs(r-l)>precision)` 
> another way to terminate, just use a fixed number iterations $100$ or so. 100 is good usually. log(r/precision)
> how much step to decrease or increase `l=m` or `r=m`

## Traditional Implementation

```C++
#include<bits/stdc++.h>
using namespace std;


bool binary_search(int a[], int n, int x){
	int l=0,r=n-1,m;
	while(l<=r){
		m = l + (r-l)/2;
		if(a[m] == x){
			return true;
		}else if(a[m] > x){
			r = m-1;
		}else{
			l = m+1;
		}
	}
	return false;
}

int main(){
	ios_base::sync_with_stdio(false);
	cin.tie(NULL);
	int n,k;
	cin >> n >> k;
	int a[n];
	for(int i=0;i<n;i++){
		cin >> a[i];
	}
	sort(a, a+n);

	while(k--){
		int x;
		cin >> x;
		cout << (binary_search(a,n,x)?"YES\n":"NO\n");
	}
	return 0;
}
```

## Alternative Implementation 

> note also works for last true 

```C++
#include<bits/stdc++.h>
using namespace std;


bool binary_search(int a[], int n, int x){
	int i =0;
	for(int j=n/2;j>=1;j/=2){
		while(i+j < n && a[i+j]<=x){
			i+=j;	
		}
	}
	return a[i]==x;
}

int main(){
	ios_base::sync_with_stdio(false);
	cin.tie(NULL);
	int n,k;
	cin >> n >> k;
	int a[n];
	for(int i=0;i<n;i++){
		cin >> a[i];
	}
	sort(a, a+n);

	while(k--){
		int x;
		cin >> x;
		cout << (binary_search(a,n,x)?"YES\n":"NO\n");
	}
	return 0;
}
```
## First Element Implementation

```C++
#include<bits/stdc++.h>
using namespace std;


bool binary_search(int a[], int n, int x){
	int l=0,r=n-1,m;
	while(l<r){
		m = l + (r-l)/2;
		if(a[m] >= x){
			r = m;
		}else{
			l = m+1;
		}
	}
	return a[r]==x;
}

int main(){
	ios_base::sync_with_stdio(false);
	cin.tie(NULL);
	int n,k;
	cin >> n >> k;
	int a[n];
	for(int i=0;i<n;i++){
		cin >> a[i];
	}
	sort(a, a+n);

	while(k--){
		int x;
		cin >> x;
		cout << (binary_search(a,n,x)?"YES\n":"NO\n");
	}
	return 0;
}
```

## Last Element Implementation

```C++
#include<bits/stdc++.h>
using namespace std;


bool binary_search(int a[], int n, int x){
	int l=0,r=n-1,m;
	while(l<r){
		m = l + (r-l+1)/2;
		if(a[m] <= x){
			l = m;
		}else{
			r = m-1;
		}
	}
	return a[l]==x;
}

int main(){
	ios_base::sync_with_stdio(false);
	cin.tie(NULL);
	int n,k;
	cin >> n >> k;
	int a[n];
	for(int i=0;i<n;i++){
		cin >> a[i];
	}
	sort(a, a+n);

	while(k--){
		int x;
		cin >> x;
		cout << (binary_search(a,n,x)?"YES\n":"NO\n");
	}
	return 0;
}
```

