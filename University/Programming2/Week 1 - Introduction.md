#OOP #Object-oriented-programming 
Slight difference between Structure programming language(C) and C++:
+ A class in C++ can contain methods(function) which are capable of manipulating data which are also defined in the same class
+ Inheritance: reuse data, methods, properties from other class 
+ Polymorphism: Multi form/views for one object
	+ Allow objects of different classes to be treated as one common base class
		+ 2 Types 
			+ Compile time Polymorphism:
				+ Function Overloading
				+ Operator Overloading
				+ Templates....
			+ Run-time polymorphism

Abstract data type : similar to struct
In C++, class is an abstract data type
	`class Student
	` Student a;

### Overview of C++
Non Object-Oriented Extension to C
+ Major improvement over C
	+ Stream I/O : cout | cin
	+ Declarations
	+ Parameter passing by reference
	+ Default argument values

Mechanism to call a function
It go through a flow then temporarily stop at certain points to start executing another function
After it finish it return back to the point where it stopped before to continue the flow
![[Pasted image 20250306080641.png]]

## Why use I/O streams
➢ Streams may be faster: printf interprets the language of '%' specs, and chooses (at runtime) the proper low-level routine. C++ picks these routines statically based on the actual types of the arguments. 
➢ Streams are extensible; I/O mechanism is extensible to new user-defined data types
### Using "fstream"
- Input/output stream class to operate on files.
```C
#include <iostream>
#include <fstream>
int fileSum(); 
int fileSum() { 
	std::ifstream infile("Ex2file");  // reading input from files
	int value, n; 
	int sum=0; //Read the number of integers 
	infile>>n; //Read members 
	int i=0; 
	while (i>value){
		infile>>value; // INPUT
		sum=sum+value; 
		i++;
	} 
	infile.close(); 
	return sum; 
	}
```
#### Declarations:
Difference C | C++ 

| C \| standard C compiler                                                                         | C++                                                                                       |
| ------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------- |
| Variables have to be declared at the beginning of the code block \| at the start of the function | Can be declared any place in the function \| main, no need to declare it at the beginning |
```C
void test(){
	int x,y;
	y = g(x); // a random function
	for(i = 0; i < 10; i++){ // might be error since i hasnt been declared
	}
}
```
### Default Arguments
- Parameters can be assigned default values 
 ➢ Parameters assume their default values when no actual parameters are specified for them in a function call
 ```C++
 #include 
 using namespace std; 
 int sum (int lower, int upper=10, int inc=1) {  // default arguments
	 int sum = 0; 
	 for (int k = lower; k <= upper; k+= inc) 
		 sum += k; 
	return sum; 
} 
main() { 
cout << "Sum of integers from 1 to 10 is " << sum (1); }//ex6-defaultarg.cpp
```

### Pass by reference
```C
#include <iostream>
using namespace std; 
int incrementByRef(int &); 
void main() { 
	int z = 9; 
	cout << "z = " << z << " before incrementByRef\n"; 
	incrementByRef(z); // DONOT have to include & TO PASS address like C
	cout << "z = " << z << " after incrementByRef\n"; 
}	
int incrementByRef(int &a) { 
	return a += 10; // caller's argument modified 
}
```

SLIGHT DIFFERENCE IN C / C++

| Feature       | C++ (Pass by reference)    | C ( pass by pointer)   |
| ------------- | -------------------------- | ---------------------- |
| Syntax        | \|`void func(int &x)`\|    | `void func(int *x)`\|  |
| Dereferencing | No need                    | Required (*x)          |
| Readability   | More readable              | explicit dereference   |
| Safety        | Less risk of Null pointer  | Check for null pointer |
| Flexibility   | CANNOT reassign references | Can reassign pointers  |

### Different type of pointer declaration
```C++

void diffConstant(){
    //Constant pointer       points to an INT
    int x = 18;
    int *const myPtr = &x; // This mean the address is constant --> only using this address to store
    //     the different value --> attempting to assign a new address
    //   ==> crashh
    // EXample: CORRECT : *myPtr = 10;
    //          INCORRECT : myPtr = &y; --> since this can not reassign to point another address
    
    ////////////////////////////////////////


    //Pointer to Constant
    int y = 11;
    const int *myPtr1 = &y; // The data is constant --> myptr is pointing to const int

    //     CANNOT modify value y via myptr
    // EX : INCORRECT *myPtr1 = 11;  ==> WRONG
    //      CORRECT:   int temp = 18;
    //myPtr1 = &temp; --> reassign pointer to point to the new address && new value


    ////////////////////////////////////////
    int z = 2005;
    const int *const myPtr2 = &z; // Data & Address are constant -> neither of them can be modified
    // const pointer (myPtr2) points to const int
    // This mean we cant do both of reassignment from above
    // to change the value hold by myPtr2
    // change Z or any pointer points to Z


    // NOTE that: change happen directly to the variable x/y/z
    // will also change the value hold by the pointer
    // Since it hold the address of the variables
    // Basically, based on differeny type of constant we can or cannot change value and address of the pointer
```

### Some brand-new Operator
- The **new** operator is used to allocate memory dynamically
#new #pointer 
```C
int *p; 
p = new int; 
*p = 15; 
int * array = new int[50];
```

- The **delete** operator is used to deallocate memory space (**created** **dynamically**)
```C
delete p; 
delete [] array;
```

-  A **jagged array**, also known as a **ragged array** or **irregular array** is an array of arrays of which the member arrays can be of ==different lengths==, producing rows of jagged edges when visualized as output.
- Applications 
	- To store an array of strings (e.g. our names) 
	-  Efficient storage for graph
![[Pasted image 20250305235938.png]]

### Marginal Difference between New(C++) vs Malloc/Calloc (C)

| Feature                               | `new` (C++)                   | `malloc` (C)                           | `calloc` (C)                           |
| ------------------------------------- | ----------------------------- | -------------------------------------- | -------------------------------------- |
| **Type Safety**                       | Yes (returns typed pointer)   | No (returns `void*`, requires casting) | No (returns `void*`, requires casting) |
| **Initialization**                    | Yes (default, value, or zero) | No (garbage values)                    | Yes (zero-initialized)                 |
| **Failure Handling**                  | Throws `std::bad_alloc`       | Returns `NULL`                         | Returns `NULL`                         |
|                                       |                               |                                        |                                        |
| **Deallocation**                      | `delete` / `delete[]`         | `free()`                               | `free()`                               |
| **Supports Constructors/Destructors** | Yes                           | No                                     | No                                     |
New  :
-  **Language:** C++ (not available in C)
- **Returns:** A pointer of the specified type (no need for type casting)
