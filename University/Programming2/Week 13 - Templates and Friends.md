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
template void display(const T & val, osteam &os) { 
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
template long indexOf( T searchVal, const T * table, unsigned size ) { 
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

