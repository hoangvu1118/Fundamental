### Some efficient strategy
#### Greedy Algorithm
#### Divide and Conquer algorithms
#### Dynamic Programming

>[!Tip]
>When searching for a solution, we may be interested in two types:
>+ Either looking for optimal solution
>+ Interested in a solution which is *good* enough, where good enough is defined by a set of parameters


Any problem maybe solved in multiple ways
--> Simplest approach is to **brute force**

### Require following definitions:
+ A **partial solution** is a solution to a problem which could possibly be extended
+ A **feasible solution** is a solution which satisfies any given requirements

--> **Brute-force search** tests all *feasible solutions*
Most techniques will build **feasible solutions** from **partial solutions** and thereby test only a subset of all possible feasible solution

## Two problems
The first requires an exact optimal solution 
	• Examples: sudoku, finding password 
The second requires only an approximately optimal solution 
	• Examples: Optimization
	
In the second case, it would be **desirable**, but **not necessary**, to find the exact optimal solution.

# Greedy Algorithm
A greedy algorithm is an algorithm which has: 
• A set of partial solutions from which a solution is built 
• An objective function which assigns a value to any partial solution

Then given a partial solution, we 
• Consider possible extensions of the partial solution
• Discard any extensions which are not feasible
• Choose that extension which minimizes the object function

>[!Tip] Note:
>Some algorithm-design technique, 
>+ Some problems, appropriately designed greedy may find either *optimial* or *near-optimal* solutions
>+ Other, greedy may perform poor or even no result at all



# Divide and Conquer Algorithm
We have seen 4 divide and conquer algorithms:
+ Merge Sort
+ Quick Sort
+ 3$^n$ Calculation
*The Steps are*:
+ A larger problem is broken up into smaller problems
+ The smaller problems are recursively
+ The results are combined together again into a solution
Thus, just using a divide-and-conquer algorithm does not solely determine the run time 
**We must also consider** 
• The effort required to **divide** the problem into **two sub-problems** 
• The effort required to **combine** the two solutions to the sub-problem

>[!important] 
>More formally, we consider those algorithms which: 
>• Divide a problem into b sub-problems, each approximately of size n/b 
>	+ In merge sort, b = 2
>	+ In 3$^n$, b = 2

# Summary
Brute Force 
• We consider all possible solutions, and find that solution which is optimal 

 Greedy algorithms 
 • We extend a partial solution to a feasible solution 

Divide-and-conquer algorithms 
• We divide a problem to many sub-problem
