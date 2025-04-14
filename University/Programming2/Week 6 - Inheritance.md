![[Pasted image 20250408080354.png | 500]]
➢Inheritance is a mechanism for expressing similarity 
➢Inheritance is a natural property of classification 
➢Inheritance is a mechanism that allows (a class) A to inherits properties of (a class) B

## Inheritance in OOP
Assume "A inherits from B". Then objects of class A have access to all attributes and methods of class B w/o the need to redefine them
```Cpp
#include <iostream>
#include <string>
class Student {
	protected:
	    std::string name;
	public:
	    void setName(const std::string& n) {
	        name = n;
	    }
	    std::string getName() const {
	        return name;
	    }
};
class DSstudent : public Student {
	private:
	    int numberCourse;
	public:
	    // You can also add methods to work with numberCourse if needed
};
int main() {
    DSstudent a; // class DSstudent now can access attribute in Student
    a.setName("Hoang");
    std::cout << a.getName();
    return 0;
}
```
Student : Superclass 
DSstudent: sub class

![[Pasted image 20250408155541.png | 400]]
**Classification** is how we define a **class** that acts as a blueprint for creating **objects**.
## Aspects of Subclasses
**Modifiability**: 
+ The degree of modifiability determines how attributes and methods inherited from a superclass can be modified in a subclass.
**Attributes**: 
>are **strategies or levels of attribute redefinition** in the context of **modifiability in OOP**, especially **attribute modifiability in class hierarchies**.

1. No redefinition: modification is not allowed 
2. Arbitrary redefinition: redefinition without constrained is allowed 
3. Constrained redefinition: the domain of attributes is constrained 
4. Hidden redefinition: definitions of attributes are hidden in subclass to avoid conflicts
This is like we have private/ protected/ private so that we can control the access of other subclasses

## Naming conflicts
*Conflicts between a superclass and a subclass*
+ When attributes or methods defined in a subclass has the same names as attributes or methods defined in the superclass
+ This is resolved by overriding

## Categories of Inheritance
**Whole/ Partial Inheritance**
+ Whole Inheritance class inherits all the properties and operations from its superclass
+ Partial Inheritance is when only some properties are inherited while others are suppressed
+ Default Inheritance: inherited properties and constraints can be modified
+ Strict inheritance: doesn’t allow the user to modify inherited properties or constraints
+ Single (simple) inheritance: 
	+  A class can inherit from one superclass only. This means the inheritance hierarchy forms a tree
+ Multiple inheritance • A class can have more than one superclass
![[Pasted image 20250414234008.png | 750]]
Overall, whole -> public | partial -> protected | strict ->private

**Multiple Inheritance**
Naming Conflicts: if **attributes or methods** defined in one superclass have the **same name as attributes or methods** defined in *another superclass*
![[Pasted image 20250408084829.png | 300]]

**Resolution**:
1. Using the order of the superclass:
	1. If more attributes or methods with the same name in different superclasses, the ones occurring in the first class in the list of superclasses are inherited (done by the compiler)
		1. Take the above picture ->> then A will use x from B1 and getValue() from B2
2. Determine by the user:
	1. The user can inherit conflicting attributes or methods, but has to explicitly rename conflicting attributes or methods in the subclass (done by the user)
	2. B1::x; or B2::x; or B3::x; 
	3. B2::getValue(); or B3::getValue()
## Abstract Class
A class without any instance --> No generating OBJECTS
➢Mammal is an abstract class: only for classification and inheritance. Never make objects of the class

+ Class A is called an abstract class *if it is used only as a superclass for other classes*. Class A only specifies properties. It is not used to create objects. Derived classes must define the properties of A.
## Summary Inheritance/Classification
 + Classification implies inheritance (whole and simple inheritance) 
 + Inheritance may effect clarity of classification (for multiple inheritance and for part inheritance)