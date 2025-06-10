For the fibonnacci problem, we take the result store it in array and use it for latter calculation
>[!Tip] Definition
>It is an algorithm design paradigm 
>• like divide-and-conquer is an algorithm design paradigm. 
>Usually it is for solving optimization problems 
>	• eg, maximumvalue, shortest path 
>	• (Fibonacci numbers aren’t an optimization problem, but they are a good example…

## **Elements of Dynamic Programming**
### 1. Optimal sub-structure: (we want to maximize or minimize sth)
+ Big problems can be broken up into sub-problems (*key characters*)
	+ Fibonacci : F(i) for i $\leq$ n
+ The solution to a problem can be expressed in terms of solutions to smaller sub-problems
	+ Fibonacci: F(i+1) = F(i) + F(i-1)
xx
### 2. Overlapping sub-problem:
+ The sub-problems overlap a lot. (*This make this algorithm difference from Divide and Conquer*)
	+ If problem is not overlap then do not use Dynamic Programming (like in Fibonacci)
	+ So by using DP --> we save time, by solving a subproblem *once* and *save* them
+ Optimal substructure. 
	+  Optimal solutions to sub-problems are sub-solutions to the optimal solution of the original problem. 
	+  Overlapping sub-problems. 
		+   The sub-problems show up again and again 
+  Using these properties, we can design a **dynamic programming** algorithm: 
	+  Keep a table of solutions to the smaller problems. 
	+  Use the solutions in the table to solve bigger problems. 
	+ At the end we can use information we collected along the way to find the solution to the whole thing

# Two ways to think about and/or implement DP algorithms

## Top down:
Think of it like a *recursive* algorithm. 
	• To solve the big problem: 
	• Recurse to solve smaller problems 
	• Those recurse to solve smaller problems • etc.. 
+ The **difference from divide and conquer**: 
	• Memo-ization
	• Keep track of what small problems **you’ve already solved** to prevent *re-solving the same problem twice*
	![[Pasted image 20250610093606.png | 400]]

## Bottom Up Approach:
![[Pasted image 20250610093902.png | 300]]
```c
int Fibonacci( int N ){ 
	int i, Last, NextToLast, Answer; 
	if( N <= 1 ) return 1; 
	Last = NextToLast = 1; 
	for( i = 2; i <= N; i++){ 
		Answer = Last + NextToLast; 
		NextToLast = Last; 
		Last = Answer; 
		} 
	return Answer; 
}
```

![[Pasted image 20250610094054.png | 400]]
## **Dynamic refers to the fact that it’s multi-stage**

