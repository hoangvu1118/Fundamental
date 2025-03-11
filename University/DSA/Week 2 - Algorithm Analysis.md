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



**Ordering**
>1 < $\log_{2}N$ < N$\log_{2}N$ < N$^2$ < N$^3$ < 2$^N$ < 3$^N$

### Big-O terminology 
- O(f(n)) --> f(n) : the growth-rate function of the algorithm
	- f(n) : *upper-bound* on T(n)
- T(n) = $\ohm$ (f(n)) (growth-rate of T(n) $\ge$ that of f(n))
	- lower-bound of T(n)
- T(n) = Θ(f(n)) (growth-rate of T(n) = that of f(n))
	- T(n) = O(f(n)) and T(n) = $\ohm$(f(n))
* T(n) = o(f(n)) :  growth rate of T(n) < that of f(n)
	* Slower than the upper-bound but near there
	* T(n) = O(f(n)) and T(n) != Θ(f(n))
- T(n) = $\omega$(f(n)) : growth rate of T(n) > that of f(n)
	- Faster than minimum rate a little bit
	- T(n) = $\ohm$(f(n)) and T(n) != Θ(f(n))

