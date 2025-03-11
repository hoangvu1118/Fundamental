## 1. Algorithm Analysis
### 1.1 Abstract:
- T(N) : time complexity --> it a function with N is the input
- Count number of *abstract simple steps*
	- Not physical runtime in seconds
	- not every machine *instruction*
- Declaration costs *no-time* `int sum`

> Depends the time complexity on the size of the input array

### 1.2 Asymptotic Analysis
When n grows to very large number
- T(n) = 4n+5
- T(n) = 2$^n$ + n$^3$+ 3n
#### 1.2.1
**Rate of Growth**
- Most algorithms are *fast* for SMALL n
- External things dominate ( OS, disk I/O)
- *n is typically large in practice*
	- Database, internet, graphics

**Quadratic Growth**
Two function f(n) = n$^2$ and g(n) = n$^2$ -3n + 2
Look different around n = 0 --> however as it goes to 1 thousands --> the difference reduced to nearly 0 (identical)

>Relative difference --> calculate the percentage difference between two methods

**Polynomial Growth** 
Two function f(n) = n$^6$ and g(n) = n$^6$ - 23n$^5$ + 193n$^4$ - 729$n^3$ +1206$n^2$ -648n
Similar to *Quadratic Growth*

> Conclusion -> Only pay attention to the largest power Quad : n$^2$ and Poly : n$^k$

#### 1.2.2
**Comparison of two functions**
f(n) = 50N$^2$ + 31N$^3$ + 24N + 15
g(n) = 3N$^2$ + N + 21 + 4 * 3$^N$
![[Pasted image 20250311093847.png]]
> Easily observe that the largest term (4*$3^N$) dominate the time complexity in second function

**Here is some stats of SOME DOMINATE TERMS** when N grows
![[Pasted image 20250311094022.png]]

**ORDER OF MAGNITUDE ANALYSIS**
Measure the time with respect to *the quickest part*
![[Pasted image 20250311095141.png]]
- Ignore any constants in front of the term --> general class
- (1) grows proportionally to N$^3$
- (2) """""""""""""""""""""""" to 3$^N$ 
*Comparing algorithms* 
Determine 
- Formulars to count operations(s) of interest
- Compare **dominant terms** of formulars

**Order of dominance
>1 < $\log_{2}N$ < N <N$\log_{2}N$ < N$^2$ < N$^3$ < 2$^N$ < 3$^N$

## 2. Big-O  
### 2.1. Definition
>Algorithm A requires time proportional to f(N) - it's said to be of order f(N) or O(f(N))
> Ex: f(N) = N$^3$  | 3$^N$
```Text
Def: An algorithm is said to take time proportional to O(f(N)) if there is some constant C such for all but a finite number of values of N, the time taken by the algorithm is less than C * f(N)
```

> We can describe it as an upper-bound for the function to run
`T(n) = O(f(N)) : growth rate of T(n) <= that of f(n)`
- Exist constant c and n0 such that `T(n) <= c * f(n) With all n >= n0`
	- This mean any value smaller than n0 will make the time btw T(N) and c* f(n) fluctuate
	- at the point n0 forward: T(N) will always smaller or equal than c * f(n)
	- n0 is required to be large enough to serve this purpose

**f(N) (Growth Rate Function):** `f(N)` expresses how the algorithm's resource consumption _changes_ as `N` grows. It's not the _exact_ time or memory used, but rather a simplified representation of how that usage _scales_.
> f(n) tells you the shape of the time increase as n increases.

For example : 50N$^2$ + 31N$^3$ + 24N +15 -> O(N$^3$)
Since T(N) will always smaller than 31N$^3$ (31 is constant) --> T(n) is O(f(n)) --> T(n) = O(N$^3$)
### 2.2 Terminology
- O(f(n)) --> f(n) : the growth-rate function of the algorithm
	- f(n) : upper-bound on T(n)

- T(n) = $\ohm$ (f(n)) (growth-rate of T(n) $\ge$ that of f(n))
	- lower-bound of T(n)

- T(n) = Θ(f(n)) (growth-rate of T(n) = that of f(n))
	- T(n) = O(f(n)) and T(n) = $\ohm$(f(n)) --> not necessarily to be the same value but in the range of lower and upper bound
	- --> c1 * f(n) < T(n) < c2 * f(n)

* T(n) = o(f(n)) :  growth rate of T(n) < that of f(n)
	* Slower than the upper-bound but near there
	* T(n) = O(f(n)) and T(n) != Θ(f(n))

- T(n) = $\omega$(f(n)) : growth rate of T(n) > that of f(n)
	- Faster than minimum rate a little bit
	- T(n) = $\ohm$(f(n)) and T(n) != Θ(f(n))

### 2.3 Types of Analysis
**Three orthogonal axes**
**Bound flavor**
- Upper bound (O, o)
- Lower bound($\ohm$, $\omega$) can be ignore 
- Asymptotically tight ($\theta$)
**Analysis Case**
- Worst case (adversary)
- Average case (rarely appear)
- Best case
- "Common" case
**Analysis quality**
- Loose bound(most true analyses)
- Tight bound (no better bound which is asymptotically different)

## 3. Analyzing Code
```C
for(int i = 0; i < n; i++){ --> N times
	for(int j = 0; j < n; j++) --> N times
		sum = sum + 1;
}
```
--> T(N) = N * N  = O(N$^2$)
**Rule 1** : Single loops 
- The running time of a loop 
**Rule 2** : Nested loop 
- Analyze from the inside out. Total running time is the product of the sizes of all the loops.
*Condition* : 
Worst-case running time: the test, *plus either the then part or the else part (whichever is the larger)*
Conditional 
	if C then S 1 else S 2 
		T(n) <= time of C + MAX (S1, S2)
		    <= time of C + S1 + S
==Example==
```C
If (N == 0) return 0; 
else { 
	for (i=0; i< N; i++) sum++;
}
```
> This case else take longer time

*Consecutive statements*
**Rule 3**: Add the time complexities of each statement
If T1(N) = O(f(N)) and T2(N) = O(g(N))
- T1(N) + T2(N) = max(O(f(N)), O(g(N)))
- T1(N) * T2(N) = O(f(N) * g(N))
Only take care about *dominant part

#### Logarithms in running time
```C
for(int i  = 0; i < N )
	i = i / 2
```
Flow : 
i = N/2 -> 1
i = N/4 -> 2
.........
i = 1 --> k steps     --> 2$^k$ = N --> k = $\log_{2}N$
T(N) = O($\log n$)

#### Recursion
- Function calls its self
- Some cases are very difficult to analyze
Example :
Normal case: O(n)
Recursion: O(n)
```C
fac(n)
	if n == 0; return 1
	else return n* fac(n-1);
```

