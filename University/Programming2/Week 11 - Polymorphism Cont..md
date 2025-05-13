## Objective
### Function Overloading
The ability to give several functions *the same name* provided the parameters for each of the functions differ in either:
+ Number 
+ Type 
+ Order (in the parameter of the function)
These are called **signature**
![[Pasted image 20250513133230.png | 300]]
### Operator Overloading
Refers to the technique of ascribing new meaning to standard operators such as `+, >> , =, ..`
when used with class operands

In fact, it is way to name a function
*Using the same name with some normal operators, make the program more readable*

![[Pasted image 20250513140318.png | 450]]

`explain i = a + b` With '+' is a method inside AClass
It is similar to call `a.f(b)` but for the operator the .f() can be remove
--> a + b
The ‘+’ symbol has been overloaded to represent: 
	• integer addition 
	• floating-point addition 
	• pointer addition
**Not all operator allowed OVERLOADING**

![[Pasted image 20250513140936.png | 320]]  ![[Pasted image 20250513140950.png | 300]]

## Restriction
### Neither the precedence nor the associativity of an operator can be changed
Operators like `*` and `+` have fixed rules for **what order they’re evaluated in** (precedence) and **which side is evaluated first if they’re the same** (associativity). You can't change this.
`MyType a, b, c;
`a + b * c; // * will still be done before +`
✅ You can change what the operator does,
❌ but not when it happens in an expression.
### Default Argument cannot be used
>[!Warning] 
>If we use *operator overloading* we can not assign default value for the parameter
>Wrong --> int operator +(int a = 0);
### The arity of the operator cannot be changed
"Arity" means the **number of inputs** an operator takes.
![[Pasted image 20250513142147.png | 660]]
```cpp
Point operator+(Point); // ✅ fine (2 operands)
Point operator+();      // ❌ invalid (wrong number of operands)
```
❌ Only existing operators may be overloaded


```cpp
class Compute{
    int _x;
    public:
        Compute(int x = 0){
            _x = x;
        }
        Compute operator+(Compute& other){ // The & is not neccessary 
        //But it will reduce time on CPU --> it dont have to make acopy of 'other'
            return Compute(_x + other._x);
        }
        void print(){
            std::cout << "Value = " << _x;
        }
};
int main(){
    Compute left(24), right(50), result;
    result = left + right; // it see as left.operator+(b)
    result.print();
    return 0;
}
```