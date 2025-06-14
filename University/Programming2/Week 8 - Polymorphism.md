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
When we want to do the same action but for *different parameters*
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
Coercion usually **converts the "lesser" type to the "greater" type** to prevent loss of information. This often means:
- **Integer → Float**
- **Char → Integer**
- **Smaller type → Larger type**
- **Non-string → String (in concatenation)**
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


## Virtual Destructors
+ Calling the wrong destructor could be disastrous, particularly if it contains a *delete* statement
+ Destructors are not inherited
+ Always make base classes' destructors *virtual* when they're meant to be manipulated polymorphically

If we do not set the destructor to be virtual, then
+ When we call *delete* , it only calls the destructor from the base class 
But when we set the *virtual*, then it will call the *destructor from derived class first then the base class*


## Abstract Class

**Pure virtual Function**
```cpp
virtual return_type function_name(parameters) = 0;
```
This is a class but we *can not create a INSTANCE for it*
However, this is still a parent class that other derived class should follow
It serves as a **blueprint or a contract for derived classes**, outlining a set of methods that the derived classes _must_ implement.

A class that belongs to the type *abstract class* must have at least 1 PURE VIRTUAL function
```cpp 
#include <iostream>
// Abstract base class
class Shape {
public:
    // Pure virtual function for calculating area
    virtual double calculateArea() const = 0;
    // Regular virtual function (optional in an abstract class)
    virtual void display() const {
        std::cout << "This is a shape." << std::endl;
    }
    // Virtual destructor is good practice in base classes
    virtual ~Shape() {}
};

// Concrete derived class
class Circle : public Shape {
private:
    double radius;
public:
    Circle(double r) : radius(r) {}
    // Implementation of the pure virtual function
    double calculateArea() const override {
        return 3.14159 * radius * radius;
    }
    // Override the display function
    void display() const override {
        std::cout << "This is a circle with radius " << radius << "." << std::endl;
    }
};
// Concrete derived class
class Rectangle : public Shape {
private:
    double width;
    double height;
public:
    Rectangle(double w, double h) : width(w), height(h) {}
    // Implementation of the pure virtual function
    double calculateArea() const override {
        return width * height;
    }
    // Override the display function
    void display() const override {
        std::cout << "This is a rectangle with width " << width << " and height " << height << "." << std::endl;
    }
};

int main() {
    // Cannot instantiate an abstract class directly
    // Shape myShape; // This would cause a compilation error
    // Can use pointers or references to abstract classes
    Shape* shape1 = new Circle(5.0);
    Shape* shape2 = new Rectangle(4.0, 6.0);
    // Polymorphic calls
    std::cout << "Area of shape1: " << shape1->calculateArea() << std::endl;
    shape1->display();
    std::cout << "Area of shape2: " << shape2->calculateArea() << std::endl;
    shape2->display();
    delete shape1;
    delete shape2;
    return 0;
}
```
For the *derived class* that do not specify the implementation of the PURE VIRTUAL class, it is deemed to still be an *abstract class*

While you cannot create an _object_ or _instance_ of an abstract class directly (like `Shape s;` or `new Shape();`), you can definitely declare and use **pointers and references** to an abstract class type.
```cpp 
Shape* myShapePtr; // Declare a pointer to the abstract class Shape // Now, make it point to an object of a concrete derived class 
myShapePtr = new Circle(10.0); // Pointing to a Circle object
```
- Each derived class (`Circle`, `Rectangle`) provides its specific implementation of that interface.
- By using a pointer or reference to the base class type (`Shape*` or `Shape&`), you can hold objects of _any_ derived type.

➢ The purpose of an abstract class is to provide an appropriate base class from which other classes can inherit. Abstract classes often represent concepts for which objects cannot exist 
➢ Abstract classes cannot be used to instantiate objects and serves only as an interface. Attempting to instantiate an object of an abstract class causes a compilation error 
➢ In contrast, classes that can be used to **instantiate objects** are called **concrete classes**
## Summary
Four types of Polymorphism
• Runtime polymorphism 
• Parametric polymorphism (compile time polymer.)=>Templates 
• Ad-hoc polymorphism (Overloading) 
• Coercion polymorphism (Casting)

Inclusion Polymorphism (via Overriding)
It’s when a **base class pointer or reference** can point to objects of **derived classes**, and the correct method is chosen at **runtime** — this is done using **overriding**.

Why is it important?
**Flexibility & Extensibility:** You can write code that works on base class types but behaves differently for each derived class.
**Key to OOP Principles:** Supports the **Open/Closed Principle** — code open for extension but closed for modification.
![[Pasted image 20250614093142.png | 400]]

## Vtable
C++ (and Java) use the virtual table (vtable) mechanism to **implement dynamic binding**
• A class with **virtual member** functions has a virtual table which contains the **address** of its virtual functions 
• An object of such a class has a pointer (**vptr**) to point to the virtual table of the class 
• Dynamic binding is done by 
1. Following the vptr to reach the virtual table of the class 
2. Looking up the virtual table for the entry point of the appropriate function at run-time
3. ![[Pasted image 20250614093318.png | 200]]