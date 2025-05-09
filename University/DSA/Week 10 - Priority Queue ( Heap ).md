## Definition
With queues 
	The order may be summarized by **first in, first out**
If each object is associated *with a priority*, we may wish to *pop* that object which has *highest priority*

>[!Note]
>With each pushed object, we will associate a nonnegative integer (0, 1, 2, ...) where:
• The value 0 has the highest priority, and
• The higher the number, the lower the priority
## Implementation - Multiple queues
One for each priority
It is create an array in which, the element inside it is queue
We want to push the object with the corresponding priority
Top and Pop, we have to consider the array with highest priority,
If it is empty, continue searching for non-empty queue -> worst case O(M) M is number of priority
>[!Run time]
>The run times are reasonable:
• Push is Q(1)
• Top and pop are both O(M)
*Unfortunately*:
• It restricts the range of priorities
• The memory requirement is Q(M * n)
## AVL Trees
We could simply insert the objects into an AVL tree where the order is given by the stated priority:
• Insertion is O(ln(n))
• Top is O(ln(n)) (or Find Min)
• Remove is O(ln(n))

However, logn still not fast enough to be constant, and we aim for constant time for removing objects

## Heaps
A tree with the top object at the root
• We will look at binary heaps

### Binary Min-Heap:
>[!Tip] Definition
>A non-empty binary tree is a min-heap if
• The key associated with the root is less than or equal to the keys associated with either of the sub-trees (if any)
• *Both of the sub-trees* (if any) are also binary *min-heaps*
• Single node is a min-heap

Easy term: The smallest number of a subtree will be at the top 
This makes any keys(value) in both sub-tree are *greater than* the root key

>[!Warning] Important
>There is no other relationship btw the elements in the two subtrees

### Pop-operation
Recursively promote the subtree node to become a root 
![[Pasted image 20250506095616.png | 200]] ![[Pasted image 20250506095644.png | 200]] ![[Pasted image 20250506095701.png | 200]]

### Push - operation
First, we randomly insert a node at any leaf 
Second, we then move this node to it correct positions, by switching node
After that, check if the subtree is in correct location otherwise, move it down

![[Pasted image 20250506100424.png | 250]]![[Pasted image 20250506100442.png | 250]]

### Complete Binary Tree as Heap
It is a binary tree in which all levels are complete *except the lowest one* 
+ Maintains the balance of the binary tree
+ The height *h* of complete binary tree is O(log N)
+ By using complete binary trees, we will able to maintain, with minimal effort, the complete tree structure

>[!Tip] Difference
>Pop and Push will be different to previous in the Heap, since we can to complete tree with small effort

Push to the last node, the move it up to the correct place
Pop, we can not use the same method, since it will create a hole in a tree
then we lost the balance of a complete binary tree

### The complete Tree
We may store a complete tree using an array:
• A complete tree is *filled in breadth-first traversal order*
• The array is filled using breadth-first traversal

## Array Implementation of Min Heap
Advantages of storing a heap as an array rather than a pointer-based binary tree
+ It is easy to store a complete tree as an array and still be able to find children and parents easily.
	+ For element at array i: left child (2i), right child (2i+1), parent (i/2)
Lower memory usage
Easier memory management

**Disadvantage** is that an estimate of the maximum heap size is required in advance
If we associate an *index–starting at 1*–with each entry in the breadth-first traversal, we get:
![[Pasted image 20250506105529.png]]
>[!Tip] Notation
>Given the entry at index k, it follows that:
• The parent of node is a k/2
• The children are at 2k and 2k + 1
**Cost (trivial):** start array at position 1 instead of position 0

>[!Tip] Push strategy
>If the heap-as-array has count entries, then the next empty
node in the corresponding complete tree is at location
**posn = count + 1**
We compare the item at location posn with the item at posn/2
If they are out of order
 **Swap them, set posn /= 2 and repeat**
![[Pasted image 20250506110135.png | 300]]

If the element that is just inserted larger than its parent, swap it (move up)
![[Pasted image 20250506110248.png | 300]]
For this case, insert 8 at 23->right, but 8 smaller than 23, move it up,
then find it parent which is at (5-1)/2 => we see 12 > 8 so swap it
> [!Tip] Popping Strategy
>Since we want to *pop the one that has heighest* priority so we will remove the top, and then copy the last element in the HEAP (ARRAY) then put it on the root
>*Next*, we compare with its children, which ever smaller move up. 
>*After that*, continue comparing and move the last node down to it appropriate location, while moving up the other node.

## Runtime analysis

**Accessing** the top object is Q(1) 
**Popping** the top object is Q(ln(n))
• We copy something that is already in the lowest depth—it will likely be moved back to the lowest depth
**PUSH**
If we are *inserting* an object *less than the root* (at the front), then the run time will be *Q(ln(n))*
If we *insert* at the *back* (greater than any object) then the run time will be *Q(1)*
How about an arbitrary insertion?
• An average run time of Q(1)
![[Pasted image 20250506111407.png | 450]]
#### Binary Max Heap Similar but largest number is a root

## Heap Sort
Given an array with n numbers, **process** of **heap sort algorithm** is following:
1. Convert the array into a heap
2. Pop n items from the heap

### In-place Heapification
Starts at 0 (However, we started at entry 1 for binary heaps)
So we need different formulars
>[!Tip] Formulars:
>Children : `2 * k + 1    |         2 * k + 2`
>Parent :    (k+1)/2  - 1

### Floyd Algorithm
**Basic Idea**:
 + Start with an array of n elements
 + Start traversing *backwards* from the bottom of the tree to the top
 + Call Percolate down (or up) per each node
 ![[Pasted image 20250506112051.png | 300]]
 Even if the 95 (the largest) at the root, however, the other huge number still stay somewhere in the node, So we have to continue the search to percolate 'em'

>[!important] Heap Sort instruction on Paper - Heapify
>Firstly, Heapify the array: Either Max Heap or Min Heap
>Max Heap : Increasing Order
>Min Heap : Decreasing Order
>Start from a non-heap node - Heap node is a node that has children
>Non-Heap : just 'leaves'
>Start comparing and swapping from the *non-heap node* to the root (But have to make sure that the node we swap --> and also it children after we swap the node MUST stay in the correct space)
>Near the end, after we swap the root with its greatest child 
>Now you have to repeat the process as above, RECURSIVELY swap that root to stay in the correct location by checking its children `(2 * n || 2 * n  + 1)`
>Verify by drawing the complete GRAPH

>[!Tip] Start sorting 
>We will remove the TOP (root) and the final(last) node of the tree
>+ The root value will be inserted into the last location of the array
>+ While the last node will go to the root and begin PERCOLATE DOWN
>+ The PERCOLATION DOWN happens:
>	+ Compare the children node (`2*i || 2*i + 1) then choose the correct value
>	+ Recursively compare and swap until the the 'last' node stay in the correct space
>


