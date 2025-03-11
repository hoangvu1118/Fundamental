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
	- Any syst