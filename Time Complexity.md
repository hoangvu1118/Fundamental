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
 ```C++
 void g(int n) { 
	 if (n == 1) return; 
	 g(n-1); 
	 g(n-1); }
```
Generate up to ==O(2^n)== since each function call 2 other functions

##  Complexity Classes
![[Pasted image 20250221182456.png]]
+ O(1) The running time of a ==constant-time== algorithm does not depend on the input size.
+ O(logn) **A ==logarithmic algorithm**== often halves the input size at each step. Log2n equals the number of times n must be divided by 2 to get 1.
+ O( square root of n) ***==A square root algorithm==*** is slower than O(logn) but faster than O(n). A special property of square roots is that square root of n lies, in some sense, in the middle of the input.
+ O(n) ***==A linear algorithm==*** goes through the input a constant number of times. This is often the best possible time complexity,
+ O(nlogn) This time complexity often indicates that the ==**algorithm sorts the input**==, because the time complexity of efficient sorting algorithms is O(nlogn). Another possibility is that the algorithm uses a data structure where each operation takes O(logn) time
+ ![[Pasted image 20250221183335.png]]

