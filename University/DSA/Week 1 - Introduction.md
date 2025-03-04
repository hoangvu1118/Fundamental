```Text
1. Asymptotic Analysis 
2. Data Structures: 
	• Linear data structures: List, Stacks, Queues,… 
	• Non-linear data structures: Tree, Graph 
3. Algorithms: 
	• Basic: Sorting, Searching, Hashing 
	• Advance: Graph Algorithms (Depth first Search, Breadth First Search,
	Shortest-Path algorithms,…) 
4. Algorithm Design Techniques: 
	1. • Greedy Algorithm 
	2. • Divide and Conquer 
	3. • Dynamic Programming 
```


# Pointer
#pointer #c
- Reference to another variable (memory location) in a program
	- Change variable inside function
	- remember a particular member of a group (such as an array)
	- Dynamic (on-the-fly) memory allocation
	- Building complex data structures : linked list, stacks, queues, trees

### Basics
- Variables are allocated at *addresses* in computer memory (depends on os system)
- Name of the variable is a reference to that memory address
- A pointer variable contains a representation of an address of another variable
- ![[Pasted image 20250304095544.png]]
### Definition 
```C
Basic syntax: Type *Name Examples:
int *P; /* P is var that can point to an int var */
float *Q; /* Q is a float pointer */
char *R; /* R is a char pointer */

Complex example:
int *AP[5]; /* AP is an array of 5 pointers to ints */
//     – more on how to read complex declarations later
```

##### Address (&) 
- Address (&) operator can be used in front of any variable object in C -- the result of the operation is the location in memory of the variable
```C
Syntax: &VariableReference 
//Examples:

int V; 
int *P; 
int A[5];
// &V - memory location of integer variable V

// &(A[2]) - memory location of array element 2 in array A 
//&P - memory location of pointer variable P
```

### Pointer Variable Initialization/ Assignment
- NULL - pointer lit constant to non-existent address
	- It points to nothing
- Can initialize/assign pointer vars to NULL or use the address (&) op to get address of a variable
```C
Examples:
int V; 
int *P = &V; 
int A[5]; 
P = &(A[2]); // P points to address of the third element in array
```
### Dereference | Indirection ( * ) Operator
- refer to the contents of the variable that the pointer points to
```C
Syntax: *PointerVariable Example:

int V = 101; 
int *P = &V;
/* Then *P would refer to the contents of the variable V (in this case, the integer 101) */

printf(“%d”,*P); /* Prints 101 */
```
### Sample
```C
int A = 3; // initialize A to store value 3
int B;// also for B --> depends compiler Might be either 0 or random value
int *P = &A; // pointer P now holds the address of A
int *Q = P; // pointer Q is assigned to P --> also store the address of A
int *R = &B; // pointer R stores the address of B
Q = &B; // now pointer Q is reassigned to B, thus hold the address of B no more A
```

### Reference Parameters
- Make changes to a variable that exist after function ends
- Use **indirection** operator inside the function to change value the parameter points to
```C
void changeVar(float *cvar) { 
	*cvar = *cvar + 10.0;
}
float X = 5.0; 
changeVar(&X); // Pass by reference 
printf(“%.1f\n”,X);
```
### Pointer Return Values
- It is considerable different from pointer to function 
```C
float *findMax(float A[], int N) { 
	int I; 
	float *theMax = &(A[0]); 
	for (I = 1; I < N; I++) 
		if (A[I] > *theMax) theMax = &(A[I]); 
	return theMax; } 
void main() { 
	float A[5] = {0.0, 3.0, 1.5, 2.0, 4.1}; 
	float *maxA; // THIS is a pointer
	maxA = findMax(A,5);  // call function findMax --> maxA will point to "float" which is returned by function findMax | Technically it will store MAX's address
	*maxA = *maxA + 1.0; 
	printf("%.1f %.1f\n",*maxA,A[4]); 
}
```

Note : Slight Difference
```C
int * e[5]; // E is a 1D array of size 5 of pointers to ints | 1
int (*f)[5]; // F is a pointer to a 1D array of size 5 of ints | 2
```
To be clear :  
	1 - It is an array of 5 pointers, each element of e is pointing to an INT
Need to allocate separately
```C
#include <iostream>
int main() {
    int a = 10, b = 20, c = 30, d = 40, e = 50;
    int* arr[5] = {&a, &b, &c, &d, &e};  // Array of pointers
    std::cout << *arr[0] << std::endl;  // Output: 10
    std::cout << *arr[4] << std::endl;  // Output: 50
    return 0;
}
```

	2 - It is a pointer to an array of 5 integers | like any other normal array
```C
int main() { 
int arr[5] = {1, 2, 3, 4, 5}; 
int (*ptr)[5] = &arr; // Pointer to an array of 5 ints 
std::cout << (*ptr)[0] << std::endl; // Output: 1
}
```
### Pointers to Pointers
- A pointer can also be made to point to a pointer variable
- But the pointer must be of A TYPE that allows it to point to a pointer (similar type)
```C
int V = 101;
int *P = &V; 
int **Q = &P; /* P points to int V */ /* Q points to int pointer P */

printf(“%d %d %d\n”,V,*P,**Q); /* prints 101 3 times *
```

### Pointer Types
- Pointers are generally of the same size (enough bytes to represent all possible memory addresses
- Generally results in a Warning rather than error since C allow to do so
```C
int V = 101;
float *P = &V; /* Generally results in a Warning */
```

### Casting Pointers
- Best way to assign to different type
```C
int V = 101;
float *P = (float *) &V; /* Casts int address to float * */

Removes warning, but is still a somewhat unsafe thing to do
```

### Dynamically Allocating 2D Arrays 
- Cannot simply dynamically allocate 2D (or higher) array
- Ideas - Allocate an array of pointers (  first dimension )
	- Make each pointer point to a 1D array of desired size
--> Treat result as 2D array

# Structure in C
- A data type in a programming language is a set of data with predefined values. 
- Examples of data types are: integer, float, string,…
### User-defined data types
In C we can create structure. In C++/Java, we can create class.
``` C
For example:
struct student{
 char[20] name;
 int id;
};

struct student x; // how to declare user-defined data type
```

### Type Definition
- Syntax: typedef type Name ;
- Name becomes a name you can use for the type

```C
typedef struct student Student; 
Student x; /* x is an struct student */ 
Student* PtrToStudent

typedef char *STRING;

STRING sarray[10];

/* sarray is an array of char *’s, equivalent to declaring: 
char *sarray[10]; */
SIMILAR TO

typedef struct { 
	char[20] name;
	int id;
} Student;
```