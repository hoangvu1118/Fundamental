## **<font color="#ff0000">Binary Search</font>**
#### <u>Method 1 </u>
- Intuitive thought: Resembles looking for a word in a dictionary
	- each step halves the size of active region by half
	- If the middle position is the target --> terminate
	- Otherwise, recursively move left or right with regard to the middle element
Implementing Code:
```C++
// O(logn)
int a = 0, b = n-1; 
while (a <= b) { 
	int k = (a+b)/2; 
	if (array[k] == x) { 
		// x found at index k 
	} 
	if (array[k] > x) b = k - 1; 
	else a = k + 1; 
}
```
#### <u>Method 2</u>
- Make Jumps and slow down when it get closer to THE TARGET
- The search goes from left to right with initial jump is n/2, then n/4, n/8, .... until the length is 1
- After the jump:
	- Target has been found or
	- It does not exist in the array
```C++
int k = 0; 
for (int b = n/2; b >= 1; b /= 2) { 
	while (k+b < n && array[k+b] <= x) 
		k += b; 
} 
if (array[k] == x) { 
	// x found at index k }
}
```
