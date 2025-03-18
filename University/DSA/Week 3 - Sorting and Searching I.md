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



