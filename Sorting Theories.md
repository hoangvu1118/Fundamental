> The array  [ 1 2 2 3 5 6 8 9 ]

## $O(n^2)$  algorithm
- Ex: Bubble Sort --> swapping two consecutive elements 

**Technique to analyze Sorting Algorithm**
* *Inversion*
	* A pair of array elements (array[a],array[b]) such that a < b and array[a]>array[b], i.e., the elements are in the wrong order.
- Number of inversions: How much work needed to sort 
- Worst case: 
	- $$1+2+....+(n-1)=\frac{n(n-1)}{2} = O(n^2)$$
## O(n log n) algorithm
- Ex: Merge Sort
	1. If a = b do not do anything, because the subarray is already sorted
	2. Calculate the position of the middle K = [(a + b) / 2]
	3. Recursively sort the subarray [a.....k]
	4. Recursively sort the subarray [k+1.....b]
	5. Merge the sorted subarrays array [a....k] and array [k+1......b] into a sorted array [a.....b]
Each Recursion require O(logn) levels + Time processing each level takes O(n) time = O(nlogn)

## Sorting lower bound (quickest time to sort an array)
#### Most efficient way : O(nlogn) time
*Consider the decision tree* ![[Pasted image 20250222111938.png]]
Each node has at most 2 children --> at each stage x and y have to be compared 
	==> All possible way to sort the array ==> ***n! ways***
The height of the tree 
> ![[Pasted image 20250222112249.png]]
This yields
	![[Pasted image 20250222112315.png]]  
	Which is approximately equal to ==**nlogn**==

## Counting Sort 
#harshmap #harsh 
* Sorts an array in O(n) time assuming that every element in the array is an integer between 0...c and c = O(n).
	* Which mean if the "C" is too large --> this technique can not handle it
- This will store the number of occurrence of each number then use it as indexes
		The array [ 1, 3, 6, 9 , 9, 3, 5, 9] corresponds to 
	- ![[Pasted image 20250222112853.png]]

## Built-in Sorting Function in C++
#### Vectors: 
```C++ 
// By default --> increasing order
vector v = {4,2,5,3,5,8,3}; 
sort(v.begin(),v.end());
// [2,3,3,4,5,5,8]
```
``` C++
// Reverse Order
sort(v.rbegin(),v.rend());
// [8,5,5,4,3,3,2]
```
#### Array
```C++
int n = 7; // array size 
int a[] = {4,2,5,3,5,8,3}; 
sort(a,a+n); // sort from begin to the end of the array
```
#### String
``` C++
string s = "monkey"; 
sort(s.begin(), s.end()); // sort based on the alphabet
// "ekmnoy"
```

### Comparison Operator
* a ***comparison operator*** is defined for the data type of the elements to be sorted
#### Pair
*  sorted primarily according to their ==**first elements (first)**==. However, if the first elements of two pairs are ***equal***, they are sorted according to their ==second elements (second)==
```C++ 
vector<pair<int,int>> v; // PAIR
v.push_back({1,5}); 
v.push_back({2,3}); 
v.push_back({1,2}); 
sort(v.begin(), v.end()) // (1,2), (1,5) and (2,3).
```
### Tuple 
* In a similar way, tuples (tuple) are sorted primarily by the *first element*, secondarily by the **second element**, etc.2
```C++
vector<tuple<int,int,int> v; 
v.push_back({2,1,4}); 
v.push_back({1,5,3}); 
v.push_back({2,1,3}); 
sort(v.begin(), v.end()); // (1,5,3), (2,1,3) and (2,1,4)
```
<span style="color:rgb(0, 176, 80)"></span>
## User-defined Struct 
```C++
#include <iostream>
#include <vector>
#include <algorithm> // For std::sort
struct P {
    int x, y;
    bool operator<(const P &p) const { 
        if (x != p.x) return x < p.x;
        return y < p.y;
    }
};
int main() {
    std::vector<P> points = {{3, 4}, {1, 2}, {3, 1}, {2, 2}};
    std::sort(points.begin(), points.end()); // Uses your operator<

    for (const auto &p : points) {
        std::cout << "(" << p.x << ", " << p.y << ") ";
        // (1, 2) (2, 2) (3, 1) (3, 4)
    }
    return 0;
}
```
- The sort function use a combination of QuickSort, HeapSort, and InsertionSort
- It then picks two elements and calls "operator<" to decide which one go first
- The comparison follows these steps: 
	- If `x` is different, compare `x` values.
	- If `x` is the same, compare `y` values.
	
**Compare `(3,4)` and `(1,2)`**
- Calls `operator<({3,4}, {1,2})`
- Since `3 > 1`, return `false` → **(1,2) should come first**

> Visual of calls:
	 std::sort() → Calls operator< multiple times:
	    (3,4) < (1,2)  → false  (swap)
	    (3,4) < (3,1)  → false  (swap)
	    (3,1) < (2,2)  → false  (swap)
	    (1,2) < (2,2)  → true   (no swap)

## Comparison functions
- As