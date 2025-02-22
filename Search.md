## <font color="#ff0000">Binary Search</font>
#### Method 1 
- Intuitive thought: Resembles looking for a word in a dictionary
	- each step halves the size of active region by half
	- If the middle position is the target --> terminate
	- Otherwise, recursively move left or right with regard to the middle element

```C++
int a = 0, b = n-1; 
while (a <= b) { 
	int k = (a+b)/2; 
	if (array[k] == x) { 
		// x found at index k 
	} 
	if (array[k] > x) b = k - 1; 
	else a = k+1; 
}
```
