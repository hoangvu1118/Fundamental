## Definition and Different types of Polymorphism

### Literal Meaning
Poly : Many/different
morph: forms/ shapes

*Definition*: the ability to assign a different meaning or usage to something in different contexts


### Type of Polymorphism
+ Overloading
+ Coercion
+ Parametric Polymorphism
+ Inclusion Polymorphism or Overriding

#### Overloading
When we want to do the same action but for different parameters
```cpp
int add(int a, int b) { return a + b; }
float add(float a, float b} { return 1.0 + a + b; }
```

#### Coercion
A type of casting 
An object or a primitive is (automatically) cast into another object or primitive type (more than just overloading)
So it will typecase the first operand to follow the second operands data type 
```cpp
int add(int a, int b) { return a + b; } 
float add(float a, float b) { return 1.0 + a + b; } 
int main() { 
	std::cout << add(1, 1.0) << endl; 
}
```
Some compiler return error however, if it runs the float function will be called -> since it will typecasting 1 to 1.0

#### Parametric Polymorphism
➢Provides means to execute the same code for any type 
➢In C++ parametric polymorphism is implemented via templates.
Template -> will be executed at running time

#### Inclusion Polymorphism or Overriding
> [!Example] Polymorphism
 Different types of objects respond differently to the same function call (and same parameter types)
 This is archived by *overriding*
 We *override* an inherited function when we want to do something slightly different than what in the base class 
 Note that this highly connected to the concept of inheritance

#### Binding
>[!Example] Binding
>Connecting a method call to a method body is called binding
When binding is performed before the program is run, it is called *static/early* binding 
e.g. in C compiler
Binding occurs at *run-time*, based on the type of object, is called *dynamic/late binding*	or Parametric
Polymorphism is a concept;
Dynamic binding is a *description of how that concept is implemented*

### Static Binding
>[!Example] Code
>![[Pasted image 20250422140221.png | 300]] ![[Pasted image 20250422140244.png | 300]]
>Pointer to parent/ base class and derived class
>So pointer to parent class *can not access private method and attribute* from their derived class
>For the felid example -> it typecast the cat, tiger, ocelot to parent class/ data type 
>So they cannot access to cat, tiger ocelot private method no more
>However, the function in those derived class are just public 
>But, it is not override the function in the base class, as u can see from the terminal above


#### Dynamic Binding
>[!Code]
>![[Pasted image 20250422141643.png | 300]]
>In C++, methods are non-virtual by default. They can be made virtual by using *virtual keyword* 
>➢This design decision is due to the fact that C++ was *made to be almost as efficient as C*
> • Dynamic binding is more costly than static binding 
> • “If you don’t use it, you don’t pay for it” 
> ➢If a method cannot be overridden, it then can be statically bound (and/or made inline
> **This is OVERRIDING, when u run the code, the tiger and Ocelot will print different text**

**Virtual Function** 
• A non-static member function prefaced by the virtual keyword 
• It tells the compiler to generate code that selects the appropriate version of this function at run-time




