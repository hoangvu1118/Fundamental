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