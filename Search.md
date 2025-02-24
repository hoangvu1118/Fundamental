# ==Binary Search==
#binarySearch #binary
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
##### Additional C++ functions
<font color="#ff0000">The container has to be SORTED</font>
 ```C++
 std::vector<int> v = {10, 20, 30, 40, 50};
 auto lb = std::lower_bound(v.begin(), v.end(), target); // lowerbound
 auto ub = std::upper_bound(v.begin(), v.end(), target); // upperbound
```
Both act as two iterators ( which is similar to a pointer but it is in the container | vector, array, etc.)
- Former returns a pointer to the value of the first number who is at ==LEAST== the TARGET
- Latter returns a pointer to first element whose value is ==larger== than the TARGET

```C++
v.begin() // return a pointer to the first element of the array
auto it = v.begin();      //Doable - Dereference : *it 
                          //       - Memory address: &(*it)

v.end() // return a pointer to *one past the last element (which is invalid to dereference). Which mean after the last element 
```
Since iterators only return value of the element 
--> To get the index 
```C++
int index = lb - v.begin();  // Gives distance from first element
```
Count number of elements whose value is TARGET
```C++
auto a = lower_bound(array, array+n, x); 
auto b = upper_bound(array, array+n, x); 
cout << b-a << "\n";
```
or 
```C++
auto r = equal_range(array, array+n, x); cout << r.second-r.first << "\n";
```
<font color="#ff0000">AGAIN, THE ARRAY MUST BE SORTED</font>

#### APPLICATION OF BINARY SEARCH 
#binarySearch 
##### Find the smallest solution
```C++
int x =-1; 
for (int b = z; b >= 1; b /= 2) { 
	while(!ok(x+b)) 
		x += b; // this will terminate right after the smallest is found 
				// (b will not be added up)
} 
int k = x+1;
```
ok(x) returns true if x >= k and false if x < k   ( /\ ) just like this, the top is k
That means we can find the smallest value as soon as the ok(x) turns true
##### Find the maximum value
* Similarly, we can find the value which first increase then decrease
* Find position k such that 
	* f(x) < f(x+1) when x < k
	* f(x) > f(x+1) when x >= k

```C++
int x =-1; 
for (int b = z; b >= 1; b /= 2) { 
	while (f(x+b) < f(x+b+1))  // similar to above solution 
		x += b; 
} 
int k = x+1;
```

# ==Complete Search==
