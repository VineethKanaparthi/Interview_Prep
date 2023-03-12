> Related to [[DSA Prep]]

## Table of Contents

- [String to Integer Conversion](#string_to_int_conversion)
- [epsilon](#epsilon)
- [set precision](#set_precision)
- [custom comparator for pq's](#custom_comparator_pq)
- [checking for overflow](#checking_for_overflow)
- [[C++ Tips Tricks && Tricky Things#String Tokenization|String Tokenisation]]

#### string_to_int_conversion
```C++
int x = stoi(s);
```

#### epsilon
```C++
T epsilon = numeric_limits<T>::epsilon()
```

#### set_precision
>  [article](https://cplusplus.com/reference/iomanip/setprecision/) 
```C++
// floating precision
cout << setprecision(5) << f << endl;
// fixed preicison
cout << fixed << setprecision(5) << f << endl;
// to reset
cout << defaultfloat << f << endl;
```

#### get_line

> So when we type 2 and then hit enter, std::cin captures the string "2\n" as input. 
> It then extracts the value 2 to variable choice, leaving the newline character behind for later. Then, when std::getline() goes to extract text to name,  it sees "\n" is already waiting in std::cin,  and figures we must have previously entered an empty string! Definitely not what was intended. `ws` is a `std` variable which when used extracts all the white space;

```C++
getline(cin >> ws, name);
```

#### custom_comparator_pq

- use custom comparator function when working with pairs. it's much faster for some reason. especially when working with longs.
- example: [cses-my-submission](https://cses.fi/problemset/task/1671/)
```C++
class comp{
public:
	bool operator()(const pair<long,int>& first, const pair<long,int>& second) const {
		return first.first > second.first;
	}
};
```

#### checking_for_overflow
- he logic relies on the fact that if an overflow occurs, the sign changes and overflow only occurs if the resulting number is greater than both the numbers or if its lesser than both the numbers.

```c++
bool isOverFlowing(long a, long b){
	return (a > 0 && b > 0 && (a+b)<0) || (a < 0 && b < 0 && (a+b)<0); 
}
```

#### String Tokenization

```C++
string s;
getline(cin>>ws,s);
vector<string> tokens;
char* token = strtok(&s[0], " ");
while(token != NULL){
	tokens.push_back(token);
	token = strtok(NULL, " ");
}
```
