#OOP #Object-oriented-programming 
## Outcome:
- Describe crucial concepts in OOP
- Write simple program in C++ using variables, operators, control structures, function and I/O objects cin/cout
- Write simple programs in C++ using objects and classes
- Utilize the features of OOP such as conversion, inheritance, polymorphism to develop programs for given problems
- Develop the applications using OOP with C++

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
