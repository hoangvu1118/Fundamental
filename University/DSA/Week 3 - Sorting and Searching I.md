## Sorting : The problem space
General problem:
+ Given a set of N orderable items, put them in order
+ W/o loss of generality, assume:
	+ Items are INT
	+ Ordering is $\leq$ (increasing order) 

> [!definition]
> In-Place sorting 
> May be performed *inplace* that is with the allocation of at most $\theta$(1) *additional memory*  (eg: fixed number of local variables)

Other sorting algorithms require the allocation of second array of equal size 
+ Requires $\theta$(n) additional MEM
**CLASSIFICATION**
![[Pasted image 20250318093716.png]]

**RUN-TIME**
Three categories:
+ $\theta$(n)
+ $\theta$(nlog(n))
+ O(n$^2$)

We examine best, average- and worst-case scenarios for each algorithm
-> Some of the best case are O(N) or the worst case of it might be O(N$^2$)

## Traditional sorting algorithms:
**With time complexity : O(n$^2$)** --> Insertion sort
**Faster : O(nlogn):** ==HeapSort==, Merge Sort, Quick Sort
**Linear-time sorting**: Bucket sort, Radix Sort
+ We must make assumptions about this data for this type

### Lower-bound Run-Time
>[!Definition]
>Any sorting algorithm must be $\ohm$(n)
>--> It have to go through each element at least one

**We will not be able to achieve $\theta$(N) behaviour w/o additionoal assumptions**

## Insertion Sort
Main idea: 
+ P0, P1, P2, P3 assume they are all sorted
+ If we have an additional new number --> try to insert into the given array
>[!Example]
>34  8  64  51  32  21
>P= 1 Look at the first element only, do not change
>P = 2 --> Temp = 8
>34 > 8, so second element is set to 34
>Then we paste/insert the temp into the correct position
>P = 3 --> Temp = 64, stop at the 3rd position since 34 is smaller than 64
>P = 4 --> temp = 51, --> copy the 64 to the P =4 
>Check if 51 is bigger than 34 --> insert that 51 to the p = 4

We can image it as a reverse bubble sort, since we have to loop backward to check if there is any smaller/larger number than the current/selected number


## Number of inversions:
There are $\frac{n(n-1)}{2}$ pairs of numbers in any set of n objects
==> each pair contributes to 
+ Set of ordered pairs, or
+ set of inversions

For a random ordering, we would expect roughly half of all pairs, or
$\frac{1}{2}$ $C(2,n)$   = $\frac{n(n-1)}{4}$ = O(N$^2$) inversions
**Any algorithm that sorts by exchanging adjacent element has O(n$^2$) on average** 
So, on average --> there would be roughly $\frac{n(n-1)}{2}$ / 2 pairs would form inversions
![[Pasted image 20250318103351.png]]

### Complexity Analysis of Insertion Sort
Worst-Case: O(n$^2$) Move to all element 
Best-Case: O(n) Array has very few inversions or already increasing order
Average-Case: O(?) --> Time complexity *depends on the number of inversion* in the array
--> T(n) = O(n+d) = O(n+ $\frac{n(n-1)}{2}$) = O(n$^2$)
==Note==: If the number of inversions in an array is low, the time complexity is low

## Selection Sort
Select the smallest value in the group and bring it to the top of the list. Continue this process until the entire list is selected
34 8 61 51 21
--> 8 34 61 51 21
--> 8 21 34 61 51
--> 8 21 34 61 51
--> 8 21 34 51 61
Worts-Case: O(n$^2$) 
Best-case: O(n$^2$)
Average-Case: O(n$^2$)
**Worse than Insertion Sort**

## Merge Sort
Out-place sorting algorithm
>[!Definition]
>It is defined recursively 
>If the list is of size 1, it is sorted --> we are done
>Otherwise:
>- Divide an unsorted list into two sub-lists,
>- Sort each sub-list recursively using merge sort and then merge

RUN-TIME:
T(n) = 2T(n/2) + n
T(n/2) to do one recursive call to sort one half of the array
the other to sort right side of array
n is to combine both side

T(N) = $\theta$(nlogn)
![[Pasted image 20250318112757.png]]

**Drawback** : We need extra memory O(n)
