## Hashing process
+ We will break the process into two independent steps
We will try to get each of these down to Q(1)
Map to an index 0, ..., M– 1 
Deal with collisions:
+ Chained hashes table
+ Open addressing
	+ Linear Probing
	+ Quadratic Probing
	+ Double Hashing
![[Pasted image 20250429104543.png | 300]]

**Step 1** : Convert an object to an integer
**Step 2**: Map this integer to a value p in range `[0, M-1]`

The alphabet : might be a poor hash table, since  the size is small
--> poor distribution

### Properties that a hash function should have
a. Should be fast: ideally Q(1) 
b. The hash value must be deterministic 
	• It must always return the same an integer each time
 c. Equal keys must always hash to the same value 
	 • x = y --> h(x) = h(y) 
d. Using the whole hash table (for all 0 ≤ k < size, there’s an i such that hash(i) % size = k) 	 
e. A good distribution on hash table

### How to Design a Hash Function
• Know what your keys are 
• Study how your keys are distributed 
• Try to include all important information in a key in the construction of its hash 
• Prune the features used to create the hash until it runs “fast enough” (very application dependent)

### Collision
What do we do when two keys hash to the same entry?
– open hashing: put a linked list in each entry
– closed hashing: pick a next entry to try
– Double hashing: use two hash function

#### Open Hashing / Separate Chaining
*Put a linked list at each entry:*
 – choose type as appropriate
 – common case is unordered linked list (chain)
 *Properties*:
 -$\lambda$ can be greater than 1
 – performance degrades with length of chains
 ![[Pasted image 20250429105947.png | 150]] ![[Pasted image 20250429110039.png | 400]]

Insertion is O(1). 
Successful Search requires 1 + ($\lambda$/2) on average. 
Unsuccessful Search requires $\lambda$ on average

Worst case searching complexity depends on the maximum length of a list `H[p]` =>O(q) if q is the maximum length. 

Want $\lambda$ to be approximately 1. 
To reduce worst case complexity we choose hash functions which distribute the elements evenly in the list

#### Closing Hashing / Open Addressing
We only allow one Key at each entry:
+ Two objects that hash to the same spot can not both go there
+ First one there gets the spot
+ Next one must go in another spot
**Constraints**
+ $\lambda$ $\leq$ 1 
	+ *Number of elements $\leq$ TableSize*
	+ Performance degrades with difficulty of finding right spot

### Probing - To handle collision
![[Pasted image 20250429111956.png | 350]] ![[Pasted image 20250429112009.png | 300]]

### Searching
Start at the appropriate position, and searching forward until 
1. The item is found
2.  An empty item is found, or 
3. We have traversed the entire array
The third case will only occur if the hash table is full (load factor of 1)

### Erasing
Elements *cannot be removed naively* without affecting search correctness

Real Deletion: We remove the wanted element and then move the elements that are in wrong location ->> move them back to the correct location 
![[Pasted image 20250429113725.png | 350]]

Problems of primary clustering vs Quadratic
**Primary clustering** is when a group of **consecutive filled slots (a cluster)** forms in the hash table. As more keys are added, this cluster grows.

When new keys collide and are placed into the cluster (since they hash to somewhere inside it), they get added to the **end** of the cluster — making it **longer**.

As a result:
- **New insertions** are more likely to land near or inside this cluster.
- **Search time** and **insertion time** increase dramatically as the cluster grows.
- Performance degrades even if the load factor is not very high.
### Quadratic Probing
![[Pasted image 20250429113748.png | 340]]

### Double Hashing
Load Factor ($\lambda$) 
![[Pasted image 20250429114443.png | 340]]

Double hashing method
![[Pasted image 20250429114804.png | 400]]
Those location that has been occupied, we then calculate a *second hash function* 
The result will be the total of next move we have to move, in order to insert the value into the *hash table* 
Ex: 47 modulo 7 == 5, but 5 has been occupied
So we start calculating from the next location 6(1) -> 0(2) -> 1(3) : then 1 which is 3rd element -> will be perfect location

