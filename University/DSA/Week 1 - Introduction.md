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


# 1. Pointer
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
	return theMax; 
} 
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

### 1D Arrays and Pointers
```C
int A[5];
A is the address where the array starts | equivalent to &(A[0])
```

**`To determine the address of A[x]`** , use 2 following formulas
``` Text
Address of A + x * bytes to represent int
Address of array + element num * bytes for element size
```
- The key behind these 2 formulas is 
	1.  The first one might be used in a ==RAW pointe==r which will then <font color="#ff0000">calculated the offset by x </font>element (similar to Computer Architecture)   
		- When multiply bytes --> multiply to its elements size 
			- Ex: for int : 4 bytes | char : 1 bytes --> like array in CA 1 Word = 4 bytes
			- This is manually computing the address
			- `int *new_addr = (int *)((char *)ptr + x * size);`
			- Base Address+(Offset×Size) 
				- 0x1000 + (3×4) =0x100C
			-  So, `new_addr` now points to address `0x100C`.
			
	2. The second one is used for REAL array 
		- Calculating the address of an element by <font color="#ff0000">multiplying index by the element size</font>
		- int *element_addr = arr + element_num;              or the one above
		- `0x2000 + (2 * 4) = 0x2008`  
		- So, `element_addr` points to `0x2008` 
```C
int arr[5] = {10, 20, 30, 40, 50}; 
int offset = 2; 
int size = sizeof(int); // arr is NOT a pointer variable, so this is invalid:
arr = (int *)((char *)arr + offset * size); // ❌ ERROR!
```

```C
int arr[5] = {10, 20, 30, 40, 50}; 
int *ptr = arr; // ✅ Now ptr is a real pointer // Now we can apply the first method: 
int offset = 2; 
int size = sizeof(int); 
int *manual_addr = (int *)((char *)ptr + offset * size);
```
We still need another pointer to traverse through array in both ways
- However, C already accounted for size of the type --> we can simply do
- **array + element_num // No need to multiply by size!**

+ The + operator when applied to a pointer value uses the formula above:
```C
A + x is equivalent to &(A[x]) 
*(A + x) is equivalent to A[x]
```

##### Passing 1D Array as Parameter
- 2 Ways of passing an Array
```C
ParamName[]
or // Either way is gonna be trated as representing array
*ParamName

int totalArray(int *A, int N) { 
	int total = 0;

	for (I = 0; I < N; I++) 
		total += A[I];
return total;
}
```
==**HOWEVER**== **for multi-dimensional array**, we still have to use the form, dimension after the first one have to be specified
```C
ArrayName[][Dim2][Dim3]
```
### Dynamic Memory Allocation 
- Allow the program to allocate some variables (notably arrays), **during the program**
- Idea: user request some memory, after they finish using it, they return (free) those memory
**--> Memory allocated in the Data Heap**
### Memory Management Functions
		``Malloc | Calloc -> memory is allocated from heap``
		
```Text
calloc = routine used to allocate ARRAYS of memory
malloc = routine used to allocate a single block of memory
realloc = routine used to extend the amount of space allocated previously
free = routine used to tell program a piece of memory no longer needed

NOTE: we have to explicitly free the memory
```
malloc is slightly faster than calloc 
since malloc do not initialize, thus it only holds garbage value
while calloc is initialized with all 0

| Arrays of memory                                                                                                                                                                                                                  | Single block of memory                                                                                                                                                                                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| - A structured collection of **elements of the same type.**<br>- Can be statically or dynamically allocated.<br>- Example: `calloc(10, sizeof(int))` allocates memory for an array of 10 integers (40 bytes if `int` is 4 bytes). | - A **contiguous** region of memory allocated dynamically.<br>- Can store **any type of data** (e.g., structures, single values, arrays). - Best approach is to use Struct to store multiple data type in one block of memory<br>- Example: `malloc(100)` allocates a single block of 100 bytes. |
| implies structured storage (usually multiple elements of the same type).                                                                                                                                                          | raw allocated space                                                                                                                                                                                                                                                                              |
| [ 0 ][ 0 ][ 0 ][ 0 ][ 0 ][ 0 ][ 0 ][ 0 ][ 0 ][ 0 ]                                                                                                                                                                                | [------------------------------------]                                                                                                                                                                                                                                                           |
| Need an array or a block of memory that **must start with zero values.**                                                                                                                                                          | Intend to **immediately overwrite** it with your own data.                                                                                                                                                                                                                                       |
| SAFER                                     TradeOff                                                                                                                                                                                | FASTER                                                                                                                                                                                                                                                                                           |
| Safe to use `arr[i]` directly                                                                                                                                                                                                     | Still safe, but uninitialized                                                                                                                                                                                                                                                                    |
#### CALLOC
#calloc #memory #allocation
```C
Calloc example
It returns the address of the first byte of this memory
Return NULL if not enough memory
void *calloc(size_t num, size_t esize)
// size_t : special type used to indicate sizes, generally an unsigned int
// num : number of elements to be allocated in array
// esize : size of the ELEMENT (INT FLOAT DOUBLE)
float *nums; int N; int I;
printf(“Read how many numbers:”); 
scanf(“%d”,&N);
        // type        num         esize
nums = (float *) calloc(N, sizeof(float));
/* nums is now an array of floats of size N */ 
for (I = 0; I < N; I++) {
	printf(“Please enter number %d: “,I+1); 
	scanf(“%f”,&(nums[I]));
}

// Access as an array 
int *arr = (int *)calloc(n, sizeof(int)); // Allocates memory for 5 integers
for (int i = 0; i < n; i++) {
	arr[i] = i * 10; 
	// Safe because calloc() allocated space for n elements
```

#### Free 
```Text 
It is problematic to free an address of something that was not allocated dynamically or has been freed
```
For example :
```C
nums = (float *) calloc(N, sizeof(float));

/* when done with nums: */ 
free(nums);
/* would be an error to say it again - free(nums) */ ERROR ❌❌❌
```
If the address is not FREED ==> The memory is still occupied BUT no longer accessible
--> This is **MEMORY LEAKAGE**

#### MALLOC
```C
MALLOC EXAMPLE
void * malloc(size_t esize) // a big chunk of memory
NULL returned if not enough memory available

malloc(N * sizeof(float)) === calloc(N,sizeof(float))
```
```C
if (arr == NULL) { 
	printf("Memory allocation failed!\n"); // check 
	return 1; 
} // Unsafe if we assume it's zeroed like calloc() 
for (int i = 0; i < n; i++) { 
	printf("Before assignment: arr[%d] = %d\n", i, arr[i]); 
	// Uninitialized garbage value 
	arr[i] = i * 10; 
}
⚠ *Memory is uninitialized, leading to garbage values.*
⚠ *You still access it like an array, but you must initialize values yourself.*
```

#### Increasing Memory Size with realloc
```C
prototype: void * realloc(void * ptr, size_t esize)

ptr : pointer to a piece of memory "previously dynamically allocated"
esize : new size to allocate (no effect if esize is smaller than the size of the memory block ptr points to already)
```

```Text
FLOW: 
program allocates memory of size esize -->
--> Copies the content of the memory at the "OLD PTR", paste it in the first part of the new piece of memory
--> OLD memory is freed up
```

```C
float *nums; 
int I;
nums = (float *) calloc(5, sizeof(float)); /* nums is an array of 5 floating point values */

for (I = 0; I < 5; I++) 
	nums[I] = 2.0 * I;

/* nums[0]=0.0, nums[1]=2.0, nums[2]=4.0, etc. */
nums = (float *) realloc(nums,10 * sizeof(float));
/*
the first 5 floats from the old nums are copied as the first 5 floats of the new nums, then the old nums is released */
```
### Dynamically Allocating 2D Arrays 
- Cannot simply dynamically allocate 2D (or higher) array
- Ideas - Allocate an array of pointers (  first dimension )
	- Make each pointer point to a 1D array of desired size
--> Treat result as 2D array
```C
float **A; /* A is an array (pointer) of float pointers */ 
int I;

A = (float **) calloc(5,sizeof(float *)); /* A is a 1D array (size 5) of float pointers */

for (I = 0; I < 5; I++)
	A[I] = (float *) calloc(4,sizeof(float));

/* Each element of array points to an array of 4 float variables */
/* A[I][J] is the Jth entry in the array that the Ith member of A points to */
```

### Non-Square 2D arrays
![[Pasted image 20250304213042.png]] 
```C
float **A;
int I;

A = (float **) calloc(5, sizeof(float *));
for (I = 0; I < 5; I++) {
	A[I] = (float *)calloc(I+1, sizeof(float));
}
```
C++ is more strict about type checking than C. In C++, you _must_ cast the return value of `malloc()` or `calloc()` to the desired pointer type. Without the cast, a C++ compiler will ==generate an error.==
# 2. Structure in C
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
            // Otherwise, we will have to type "struct student x"
Student* PtrToStudent

typedef char *STRING; // declaring a string array of 10 pointer to string

STRING sarray[10];
/* sarray is an array of char *’s, equivalent to declaring: 
char *sarray[10]; */

SIMILAR TO

typedef struct { 
	char[20] name;
	int id;
} Student;
```

#### Declare Variables in Two ways
```C
// Tag declaration 
struct TagName { 
	Type1 Field1; 
	Type2 Field2; 
	Type3 Field3;
};
//Variable declaration
struct TagName temp1;
```

```C
// Type definition 
typedef struct { 
	Type1 Field1; 
	Type2 Field2; 
	Type3 Field3;

} TypeName;

//Variable declaration:
TypeName temp1;
```
```Text
	It aint need a TAGNAME if we define Typename afterall
```

### Field Selection
- Dot (.) form to refer to field of structured var
- Syntax: VarName.FieldName
+ Each field treated as an individual variable of that type
```C
void main() { 
DATE d1;
d1.month = 12; 
d1.day = 2; 
d1.year = 1970;
// OR
DATE d1 = { 12, 2, 1970 };//must follow the order it is declared inside struct
}
```

### Structure assignment
* variables must be of same type (same name)
+ values are copied one at a time from field to corresponding field
```C
DATE d1 = { 12, 2, 1970 }; 
DATE d2;
d2 = d1; /* Assignment */
```
### Structure Comparison
+ Many compilers require vars to start on even numbered (or divisible by 4) boundaries, ***unused bytes called slack bytes***
- Should not use == or !=
	- It may be due to slack bytes
	- Some bytes might no be used ( padding )
When we compare 2 structure variable --> it will compare byte by byte
--> it also compares unused byte to another bytes which might result undefined behavior 
Solution : Compare each off the fields of the structure one at a time
--> Use the (.) to compare each attribute
![[Pasted image 20250304215322.png]]
### Structure as Value Parameter (pass like normal variable)
### Structure as Return Value
```C
typedef struct { 
int id;
float gpa;
char class; 
} Student; 

void main() {

 Student s1;
 s1 = readS();
 printS(s1); 
} 

Student readS() {
	Student s; /* local */
	printf(”Enter:\n"); 
	printf(" ID#: ");
	scanf("%d",&s.id);  // scanf so we have to use & to write to the address
	printf(" GPA: "); 
	scanf("%f",&s.gpa); 
	printf(" Class: "); 
	scanf(" %c",&s.class);
	return s;
} /* local as return val */
```
So the function readS now have the same attribute as the struct Student --> it has to return all of the attributes and then assign to s1 in the main function

### Structure as Reference Parameter
- We want to modify the original variable of type Student --> reduce copy and return 
```C
void main() {
Student s1;
readS(&s1); 
printS(s1);
}
void readS(Student *s) { // s is a pointer to s1
	printf(”Enter:\n"); 
	printf(" ID#: "); 
	scanf("%d",&((*s).id));  // or &(s->id)
	printf(" GPA: "); 
	scanf("%f",&((*s).gpa)); 
	printf(" Class: "); 
	scanf(" %c",&((*s).class));
}
```
#### Other pointer selection 
```C
StrucPtr->Field /* equivalent to (*StrucPtr).Field */ 
• StrucPtr must be a pointer to a structure
• Field must be a name of a field of that type of structure
```

#### Array within Structure
```C
typedef struct {
	char name[20];
	int score[5]; 
} Student;	
void readS(Student *s){
	scanf("%20s", s->name);
	for (i = 0; i < 5; i++){
		scanf("%d",&(s->score[i])); // access the address since score[i]-INT
	}
}
```
Slight difference in ARRAY and Pointer
- Array as pointer in C
	- When use name without index - =="s->name"== - it decays ( implicitly convert) to a pointer points to first element --> name === &name[0]
	- Since name is a pointer so no & is needed to get the address
- But in score, we getting each element, which is integer, score[i] 
	- Providing the & give the address of the location in array that need to be stored
NOTE: 
If we write "s->score" --> treated as pointer 
However, it depends on the scanf which will decide how the input will be
- For "%s" --> it will scan char until it find a "whitespace" so array would be 'h', 'o', 'a', 'n', 'g'
- For "%d" --> it will scan the integer --> therefore array would be '123',' ', ' ', ...
	- Instead of '1', '2', '3'

### Nested Structure 
```C
typedef struct { 
char B;
float C; 
} MyDType;

typedef struct { 
	int A; 
	MyDType D; // D is a variable
} MyType;

MyType V;
// Fields of V:
V.A /* int field */
V.D /* structure field */ 
V.D.B /* char field */ 
V.D.C /* float field */

or MyType V = { 43, { ‘A’, 3.5 } };
```
![[Pasted image 20250304230154.png]]
# Application of Struct
##### Representing Table Data 
To store information of each students (ID, Class, Name, GPA) we need to create a struct
We would like to keep the values for each entry in the table together as one unit
**--> Array will be a TABLE to store these students information (Struct)**
```C
include <stdio.h>
#define MAXSTUDENT 100

typedef struct { 
	int id;
	float gpa; 
	char class;
	char name[20]; 
} Student;

void main() {
	Student Ss[MAXSTUDENT]; 
	int numS = 0; // INT var to keep track of how many of the array elements are in use: == How many students are being recorded
	int option;
}
```
![[Pasted image 20250304230937.png]]

## Pointer Arithmetic

### Topic relating to 2D array
#### Application of pointer to pointer
 - It can be used to create a 2D array
```C
int (*printArr)[col] = array; // Similar to create an ARRAY of pointers to INT
```
- This is because an ARRAY is a pointer itself --> each element will be arrays that decays into pointers
- This form a 2D array

#### Accessing 2D array via pointer
First method : using Array notation `arr[row][col`
Second method : using arrow
- Flow : pointer printArr is a pointer to "col" integer
	- `printArr + i`: it will access the address of the element at `arr[i]` of col (j)
	- `*(printArr+i)` : dereference this will give the address of col(j) which is the address of a pointer to integer mentioned above
	- `*(printArr+i) + j` : give the address of the j-element in the i-th row
	- `*(*(printArr+i)+j)` : give the value at the desired position

```C
 int (*printArr)[col] = array; // Similar to create an ARRAY of pointers to INT
    for(int i = 0; i < row; i++){
        printf("Element(s) at row [%d]: " , i+1);
        for(int j = 0; j < col; j++){
            printf("%d | ", *(*(printArr + i) + j));
        }
        printf("\n");
    }
```
