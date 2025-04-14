## Addition of Two Polynomials
*Similar to merging two sorted lists*
![[Pasted image 20250408092229.png | 450]]

Solution: Take 3 pointers - 1 for blue, 1 for red, 1 for green
compare the exponent -> if equal -> add up 
otherwise -> move pointer and copy the node from that linked list

## Doubly Linked List
A node contains 2 pointers: to previous node and next node
**Move both directions**

## Circular Linked List
Last node points to first one. It can be done with doubly linked list
Ex: A university with 2500 courses and 40000 students to generate two types of reports: list of student each course + list of courses of each students
--> Multi-List
![[Pasted image 20250408094408.png | 400]]

 The reason why apply circular linked list in this case
 -> We want to save space -> so S1 is the only place to store students data -> other node from s1 only store the grade of that students
 So if we want to check the students info -> traverse a full circle and go back s1 to retrieve the data.
 -> Similar to course name -> only the header that holds the course info

## Stack ADT
LIFO : Last in First OUT
Stack is a *list* where u can access add or delete elements at one end.
The last added element will be accessed or deleted
*Operations*:
+ Stack CreateStack()
+ int isEmpty(Stack S)
+ ElementType Pop(Stack S) : delete the element at top of a stack
+ void Push(Stack S, ElementType X): Add an element X at top of a stack
+ ElementType Top(Stack S): Access the element at top of a stack
>[!Warning]
>normally, a "top" index inside a struct Stack is used to track the current index of the Stack
>If top == -1 -> Stack is empty
>top == size -1 -> Stack is full
>When we push -> top increase by 1
>pop -> top decrease by 1



## Stack Implementation
Array vs Linkedlist -> We chose Array
+ Need to know maximum number of elements
+ Delete/ Access/ Add at the end
+ O(1) Operation
	+ Store array length in the 0th position
	+ Delete/Access/Add at `A[array lenght  + 1]`
![[Pasted image 20250408100721.png | 100]]

LINKLED LIST IMPLEMENTATION of stack
No need to know the maximum size
add/ access/ delete in the beginning, O(1)
![[Pasted image 20250408100828.png | 300]]
![[Pasted image 20250408101129.png | 400]]

## STACK APPLICATION in coding
### Function Calls 
Put parameters in stack 

### Decimal to Binary Conversion
### Mathematical Expression
+ Symbol Matching
+ Evaluation of Postfix Expression 
	+ ![[Pasted image 20250408041043.png | 300]]
	+ Similar to one of the leetcode problem
+ Infix to Postfix Conversion
## Queues ADT
It is also a list,  an element is inserted at the end, but deleted from the beginning 
FIFO : First in First OUT
![[Pasted image 20250408041358.png | 350]]
### Basic Operations of Queue
+ Queue CreateQueue()
+ int isEmpty(Queue Q)
+ ElementType Dequeue(Queue Head) : delete element at head of a queue
+ void Enqueue(Queue Tail, Elementtype X) : Add an element X at tail of a Queue
### Linked List Implementation
Insert at the end of the linked list 
	Maintain a pointer to the last element.
	Whenever there is insertion, update this ``last`` pointer to point to the newly inserted element. 
Delete from the beginning of the list 
Both insertion and deletion are O(1)

**We need 2 pointers** : Actually we dont need -> but it requires more time to traverse to the end -> to add new value
## Deque ADT
![[Pasted image 20250408043036.png | 350]]


