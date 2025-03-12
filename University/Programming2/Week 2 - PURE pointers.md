## 1. Pointer to Array Elements
Pointer is related to a type or a class
**Pointer arithmetic** : Pointer pointing to an array can be incremented or decremented
```C++
float flist[] = {10.3 , 13.2, 5.5, 9.7};
float *p = flist; // p = &flist[0]
int *q;
char *r, *q1;
q = p + 4; // q = &a[4] this is because it skip 4 int 
r = (char * )p // ok
q1 = r + 4; // q1 = &a[2] --> since it is char , ""assume int = 2 bytes ""
            // each char is 1 bytes --> skip 4 char
cout << *p;
```

## 2. Void pointers
To obtain flexibility of types
We have to cast the type (INT, FLOAT, etc.) to this pointer 
Example:
```C++
int *p;
void *v = p;
p = (int*) v // cast is needed
```

### 2.1 Allocating Memory
Fragmentation : Not actually an error
- **External fragmentation:** Occurs when there's enough total free memory, but it's not contiguous.  --> it is not used effectively
- **Internal fragmentation:** occurs when allocated memory is larger than the requested memory.
- **Fragmentation errors:**
    - Problems can arise during this process:
        - Fragments can be lost or corrupted during transmission.  
        - Reassembly can fail, resulting in lost or incomplete data.  
        - Security risks can arise, as firewalls have difficulty filtering fragmented packets.

#### New operator
#new #pointer 
Initialize a pointer to point to an array 
```Cpp
int *p = new int[5];
free(p)
```
Initialize a pointer to pointer -> each element point to an array
```Cpp
int** arr = new int*[5]; // Allocate an array of 5 int pointers

for (int i = 0; i < 5; i++) {
    arr[i] = new int[4]; // Allocate an array of 4 integers for each row
}
for (int i = 0; i < 5; i++) {
    delete[] arr[i]; // Delete each row
}
delete[] arr; // Delete the array of pointers
```


# 2. Introduction to OOP
## 2.1 Solving a programming Problem
4 Pillars: Analysis --> Design  --> Coding --> Management 
Tools: Programming paradigms --> programming language

### 2.1.1 Thinking methodology 
**Induction** 
- From specialization to generalization
- e.g, to create the (abstract) concept "Bus" from different bus

**Deduction**
- From generalization to specialization
- From a class bus --> create school bus, .... any type of bus

### 2.1.2 Concepts and <font color="#f79646">Relationships</font>
- A rectangle <font color="#f79646">uses</font> lines
- A Circle<font color="#f79646"> is an </font>ellipse
- A wheel <font color="#f79646">is part of</font> automobile
- A set <font color="#f79646">creates it</font>s elements

**Approaches in Software Development** 
- Top Down approach
	- A single module will be split into several smaller modules
	- General to Specific
- Bottom Up approach
	- Lot of small modules will be grouped to form a single large module
	- Specific to General

If the requirements *are clear at the first* instance we can go for <u>Top-Down approach</u>
If circumstances where the *requirements may keep on adding*, we go for <u>Bottom-Up approach</u>

Some combinations:
Requirements : Clear + Solution : Clear --> Top-Down
             Unclear                Unclear --> 
             Clear                     Unclear --> Bottom-up | Top-down --> meet the team frequently

**Structured Programming**
- Using function 
**OOP Significant**
- A thinking methodology
	- Everything is an object
	- Any system is composed of objects ( a system is itself an object) : education system
	- The evolution and development of a system is caused by the interaction of objects

+ Objects have both data and methods 
+ Objects of the same class have the same data elements and methods
+ Objects send and receive messages to invoke actions

**Key idea in object-oriented** : the real world can be accurately described as a collection of objects that interact.

**Object-orientation support**
- Induction: object -> a class
	- Tools to do this automatically
- Deduction: a class -> objects
	- Usually done by programmers
- Top-Down : from a super class to sub-classes
- Bottom-up : from sub-class to super-class

### Why OOP?
It supports 
- Easy representation of 
	- Real-World objects
	- Their states and Abilities
- Save development time (and cost) by reusing code 
	- Once an object class is created it can be used in other applications

**FOUR main design principles of Object-Oriented Programming**
- Abstraction
- Encapsulation
- Polymorphism
- Inheritance

**Abstraction**
Implication details is hidden away --> fact about the problem at hand to design, produce and describe so that it can be easily used without knowing the details of how it works
--> Drive a car -> don't have to know the gasoline and air are mixed and ignited

**Abstract Data Types (ADT)**
In ADTs, define the interface to data abstraction w/o specifying implementation details
It includes the following properties
- It exports a type
- Exports a set of operations
- Axioms and preconditions define the application domain of the type

+ Showing only essential features and hiding the unnecessary features
+ Access modifiers in C++ or any OOP language provides abstraction
+ Function also provide abstraction || We only care to know the input and output
+ If a variable is declared as private, then other classes cannot access it
		or public --> it is contrast with the above
>Ex: Stack, Linked list -> constructed with class --> use w/o exposing how it is implemented

**Encapsulation**
+ The process of bringing together data and method of an object is called as encapsulation
+ The data and method are given in the class definition
+ Classes provides us with this feature - Encapsulation
**Inheritance**
+ Allows code reusability, which a new abstract data type can be inherit the data and functionality of some existing type and is also allowed to modify some of those entities
+ *Terminology*
	+ Class : abstract data type in OOP
	+ Object : a class instance
	+ Derived class (subclass) : A class that is defined through inheritance from another class
	+ Parent class(superclass) : A class from which a new class is derived
	+ Methods: The subprograms that define the operations on objects of a class
	+ Messages: 

**Polymorphism**
Poly : many
Morph: form 
--> Polymorphism --> coexist in more than one form
Meaning: the ability to response differently to the same message or function/method call
C++ supports **function overloading** and **operator overloading** to implement polymorphism