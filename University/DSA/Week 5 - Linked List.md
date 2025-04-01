Abstract Data Types (ADT : Lists

## Usual Data Types
Integers, Double, Boolean
--> Do not need to know the implementation

>[!Definition] 
>Data Structure: A construct that is defined in a program to store collection of data

ADT: mathematical description of a data structure(or an object) and the set of operations on the data structure (or the object)

+Implement the data structure once in the program
• Implement these operations of this data structure once 
• Use these operations again and again without going into the implementation 
• Ex: List, Set, Graph,

==Note== : An ADT may use a different ADT

**List ADT**
![[Pasted image 20250401111102.png | 450]]

### Array Implementation
+ List can be implemented as an array
+ Need to know the **maximum number of elements** in the list at the start of the program 
+ Adding/Deleting an element can take *O(n) operations* if the list has n elements. 
+ Accessing/changing an element anywhere takes O(1) operations independent of

In C we have to specified the LEN of an array if we declare it alone
>[!code]  int a[10];

### Adding an element
Normally first position (a[0]) stores the current size of the list 
	Actual number of elements currsize + 1
Adding at the beginning:
	Move all elements one position behind
	Adding at position 1, increase the currsize by 1
	![[Pasted image 20250401112104.png | 300]]
### Adding at the end
Increase the element currsize by 1 
add the element at the end
![[Pasted image 20250401112151.png | 300]]
O(1)

### Delete an Element
**Delete at beginning** :
 + Delete first element -> move all element 1 position ahead
 + Decrease size by 1
 + ![[Pasted image 20250401112320.png | 300]]

![[Pasted image 20250401112401.png | 400]]

>[!Warning] Limitation of Arrays
>• An array has a **limited number of elements** and the **size must be known** before using.– routines inserting a new value have to check that there is room 
>• **Insertion/ Deletion** is complex. We need to shift the existing elements. 
>• A better approach: *use a Linked List*

## Linked List
### Dynamically Allocating Elements
+ Allocate elements *one at a time as needed*, have each element keep track of the next element 
+ Result is referred to as linked list of elements, track *next element with a pointer*

### Components
+ Consists of **sequence** of nodes
+ Two elements:
	+ Value of the corresponding element in the list (data)
	+ Pointer to the next node
>[!Highlight]
>The pointer is a **null pointer** for the **last element.** 
>May be a special node at the *beginning*, known as the *header node*
![[Pasted image 20250401112957.png | 450]]

### How to add an element at the beginning of a linked list
![[Pasted image 20250401113558.png | 250]]           
So create a new node that has the data u want to insert
the pointer from that node points to the former-first element of the list
now the header points to that new node -> create a linked list with n+ 1 element

```Pseudocode
Create(newnode); 
Newnode->next --> L->next 
L->next --> newnode;
```
IF we want to reduce the time complexity of insert at the end from O(n) to O(1)
Create a pointer that keep track of the linked list element ---> when we add the final element to the list -> the pointer also points at that
--> when add another new element -> O(1)

