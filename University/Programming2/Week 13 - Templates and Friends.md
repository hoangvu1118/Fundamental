## Objectives
+ ADT
+ Encapsulation 
+ Inheritance
+ Polymorphism
	+ Coercion
	+ Overriding
	+ Overloading
	+ Templates

## Templates
+ Templates give us the means to define a **family** of functions or classes that share the same functionality but which may differ with respect to data type used internally
+ A function template is a framework for generating related functions
+ A class template is a framework for generating the source code for any number of related classes
A function can be defined in terms of an unspecified type
The **compiler** generates **separate** versions of the function based on the type of the **arguments passed** in the function calls

## Function template
```cpp
template <class T>
return-type function-name(T param) // one parameter function
///T is called a template parameter
```

### One Parameter Function Template
```cpp
template <class T>
void display(const T &val) { 
	cout << val;
}
```

One parameter function with an additional parameter which is note a template parameter: 
```cpp
template<class T>
void display(const T & val, osteam &os) { 
	os << val; 
} 
```

➢The same parameter appears multiple times 
```cpp
template <class T> 
void swap(T & x, T & y) {}
```

>[!Tip] When to use Overriding vs Templates
>Overriding is used when the function(internally) have different approach to do 
>--> Calculate area of each Shape (Circle, Rectangle...)
>
>Templates is used when the approach of those functions **are the same**
>
>Overloading is used when the approach between each function is a bit *different*

**Key different btw Overloading and Templates**
When we want the function to behave different with respect to the parameters
+ Overloading:
	+ Create multiple function with different type of parameters
+ Templates:
	+ Just need 1 function with parameters (i.e, T)
	+ Then pass in the parameter according to the requirements 
	+ No need multiple functions to tailor the polymorphism

## Table Lookup
```cpp
template <class T>
long indexOf( T searchVal, const T* table, unsigned size ) { 
	for (unsigned i = 0; i < size; i++) 
		if (searchVal == table[i]) 
			return i; 
	return -1; 
}
```
Special things --> We can pass in the *table* what ever type we want, and also the corresponding key value that we need to search
--> Then it is more easy to search without creating a new function that has the same datatype with the desired one
However, `if (searchVal == table[i]) ` If the operator might not compatible then we have to create an operator overloading

When a function template does not apply to a particular type, it may be necessary to either 
	• overloading the function template, or 
	• make the type conform to the function template

## Class Template
```cpp
template <class T>
class MyClass { 
	// using T inside (parametrically) 
}; 
MyClass <int> x; 
MyClass <Student> a;
```

**Example**
```cpp
template <class T1, class T2>
class Circle { 
	// ... 
	private: 
		T1 x, y;
		T2 radius; 
}; 
Circle<int,long> c1; // T1 will be int, T2 will be long
Circle<unsigned, float> c2; // T1 will be unsigned, T2 will be float
--> T1, T2 just placeholder, and we have to provide them with datatype(int,long..)
```

### Array class templates
```cpp
template<class T>
class Array {
	public: 
		Array( unsigned sz ); 
		~Array(); 
		T & operator[]( unsigned i ); 
	private: 
		T * values; 
		unsiged size;
};
```
This is a header 
--> now implement 
```cpp
template<class T> Array<T>::Array( unsigned sz ) {
	values = new T[sz]; size = sz; 
} 
template<class T> T & Array<T>::operator[] ( unsigned i ) {
	if( i >= size ) { 
		cout << "ERROR: array index out of bound!!!\n
		abort(); 
	} 
	return values[i]; 
} 
template<class T> Array<T>::~Array() { delete [] values;}
```
### Templates and Inheritance
A **template is not a class** 
	• A template is not inherited 
	
A class based on a template is an ordinary class 
```cpp
class t1 : public Array <int> {...}//OK!!! 
template<class T> 
class Myclass : public aClass {
//OK!!! 
}
```
Static members defined in a template are static members of the classes associated with a template 

>[!Important]
>If you want a class or function to be generic (work with different types), you must write `template<class T>` (or similar) before it.
>--> I’m writing a **template** — not a normal function or class. The type `T` will be provided later.”

What? Why? How? The result?

## Friends
A friend class is a class in which all member functions have been granted full access to all the (private, protected, and public) member of the class defining it as a friend(by instances)
The friend class is declared inside the class granting friendship

+ In normal class, a class method (A) can access a public method of another class (B) in and only if class(A) has instance inside the method in A --> Then it can access **public** in B
+ In Friend class, this is more, A can access every fking thing in B (public, protected, private)

### A friend function
Similar to friend class but this time the scope is only for a **FUNCTION**
Assume we got a class Employee
Then we have a function in main like void printSalary()
--> If we do not grand the **friend** access for printSalary --> then it cannot access to private and protected features in Employee
--> if we put **friend void printSalary()** then that function have full right to access every element in Employee class

>[!Warning]
>Non-Symmetrical
>+ c2 is friend of c1 but **c1 is not necessarily a friend of c2**
>Non-Transitive
>+ If c2 is a friend of c1 and c3 is a friend of c2, but c3 is not necessarily a friend of c1
>Not inheritable 
>+ A friend of a base class is not inherited by derived class

➢Friends diminish encapsulation and information hiding
➢Limit the use of “friends"
