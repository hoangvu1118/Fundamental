### Big-O terminology 
- O(f(n)) --> f(n) : the growth-rate function of the algorithm
	- f(n) : *upper-bound* on T(n)
- T(n) = $\ohm$ (f(n)) (growth-rate of T(n) $\ge$ that of f(n))
	- lower-bound of T(n)
- T(n) = Θ(f(n)) (growth-rate of T(n) = that of f(n))
	- T(n) = O(f(n)) and T(n) = (f(n))
* T(n) = o(f(n)) :  growth rate of T(n) < that of f(n)
	* Slower than the upper-bound but near there
	* T(n) = O(f(n)) and T(n) != Θ(f(n))
- T(n) = $\omega$(f(n)) : growth rate of T(n) > that of f(n)
	- Faster than minimum rate a bit
	- T(n) = $\ohm$(f(n)) and T(n) != Θ(f(n))
