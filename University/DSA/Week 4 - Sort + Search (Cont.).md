
## 1. Quick Sort
The difference from both of the sorting algorithm in previous question is 
It is **O(nlogn)** and **In-place Sorting**
The insertion is O(n$^2$) and In-place
The mergeSort is O(nlogn) but Out-Place

*Average-case* : O(nlogn)

### 1.1 Key Idea
Merge-Sort: We split the array into 2 smaller list based on location in the array
**Alternative**:
+ Choose an object in the array and partition the remaining objects into two groups (one for smaller + one for bigger) relative to the chosen object => **QuickSort**
+ Chosen Object is called **PIVOT**

**Steps to do**:
1. Choose a pivot element in the list
2. Partition the array into 2 parts
3. One contains elements smaller than this pivot, another contains elements larger than this pivot
4. Recursively sort and merge the two partitions

We don't have to merge it again like mergeSort since it already merged (in-place)
--> No extra space --> O(1) space complexity

### 1.2 Worst-case scenarios
>[!Note] 
>We would like the partitions to be as **equal** as possible
>And this depends on the choice of the pivot -> Quicksort run time *depends on the pivot*
>+
>Equal partitions are *assured* if we can choose our pivot as the element which is in the middle of the sorted list
>
It is not easy

**For better understanding**
Assume that the pivot chosen is the *SMALLEST* number --> then we have to move all of the list to the right and that just mean we only move/sort a single element not half of the array
![[Pasted image 20250325094826.png | 450]]

**Worst** : So either we choose the smallest or the biggest number --> Time drop to O(n$^2$)
*However*, it only happens when we **ALWAYS** choose the smallest number 
--> So as we choose the middle number every recursion, the probability to choose choose the smallest(biggest) number of that array is **SMALL**

**Alternative Strategy** Take the median of a subset of entries
For example, take the median of the first, middle, and last entries

### 1.3 Partitioning Process
First: Interchange the pivot with the last element 

Pointer1 points to the first element 
Pointer2 points to the second last element

Move P1 to the right skipping elements which are **Less than the pivot**
Move P2 to the left skipping elements which are **larger than the pivot**

Stop P1 when we encounter an element **greater or equal** to the pivot
Stop P2 when we encounter an element **lesser or equal** to the pivot

**Memory Requirements**
O(log(n)) : since on the average, we recursively split the array into two parts to deploy quicksort 
--> so those calls are made on a stack --> depth of the recursive tree is O(log(n))
In worst case, it might be O(n)

![[Pasted image 20250325104951.png | 500]]

### 1.3.1 Cutoff
Quicksort and Mergesort perform well for **Large Inputs** but not for small inputs
--> Solution
When the divisions become small, we can use **insertion sort**  to sort the small division instead. 
For example, 5 $\leq$ cutoff $\leq$ 20

## 2. BinSort (a.k.a BucketSort)
Special Case Sorting: Present **linear time** sorting algorithm 
These apply *only* when the input has **Special Constraints** 
- Inputs are INT and we already know the *min and max* of each element

**Requires**:
+ Having an array with N elements
+ Each element is in {1,...., K}
**Mechanism**:
+ Putting items into correct bin(cell) of array, based on key

![[Pasted image 20250325111524.png | 300]]


## 3 Searching
Two things that affect search algorithm selection:
+ Whether the array is **sorted**
+ Whether all the elements in the array are *unique* or have *duplicate* values
### 3.1 Linear Searching - unsorted list
#search 
Simplest way to find an element in an array 
- Check if it **matches** the sought after value

**Time complexity**
Worst-Case: O(n) the entire array must be **linearly searched**. This occurs when the value is in the *last position* or not found
Best Case: O(1) --> the element located in the first element
Average Case: O(n)  --> C(2,n) / n

### 3.2 Binary Searching - sorted list
#binarySearch 
Begin at the **middle** of the array
+ If the value is less than the middle -> check the middle item between the first item and the middle
+ If it is more than the middle item -> check the middle item between the middle and the last section
Stop when the value is found or when the remaining array of elements to search consists of one value 
**Time complexity** O(logn)

