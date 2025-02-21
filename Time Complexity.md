## Calculation Rules
+ Each loop accounts for 1 power of n which means O(n^k).
+ ![[Pasted image 20250221181010.png]]
**It shows ==THE ORDER OF MAGNITUDE==** : 3n, n+5, n/2 times will be recognized as ==**O(n) time** ==

#### Phases 
+ Complexity is the largest time complexity of a _**Single phases**_
+ 3 consecutive block of code --> O(n), O(n^2) and O(n) ==> O(n^2)
#### Several variables
``` C++
for (int i = 1; i <= n; i++) { 
	for (int j = 1; j <= m; j++) { 
	// code 
	} 
}
```
--> O(m * n)

#### Recursion
+ Time complexity depends on the number of times the function is called
```C++
void f(int n) { 
	if (n == 1) return; 
	f(n-1); 
	}
```
f(n) causes n function calls, time for each is O(1) ==> accumulate to O(n)
 ==However== 
 