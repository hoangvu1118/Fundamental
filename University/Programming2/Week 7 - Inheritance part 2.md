
## Base and Derived Classes
A base class is a previously defined class that is used to define new classes(now)
A derived class inherits all the data and function members of a base class
### Single Inheritance
Implement an "is-a" relationship
The derived class only has one base class

### Declaring Derived Classes
![[Pasted image 20250415131711.png | 500]]
opt: option
Default = Private

In order for a derived class access to private data
We have to create functions SET/GET to set the value and to get(print) those values 
```cpp
class Publisher{
	private:
		string publisher;
		int date;
	public:
		void setPublish(p):
			publisher = p
		string getPublish():
			return p;
}
Class Book : public Publisher{
	private:
		....
	public:
		set()
		get()
}
int main(){
	Book b1;
	b1.SetPublish("Oreily");
	b1.getPublish();
}
```

### Order of Constructor and Destructor Execution
**Base class** constructors are always executed first
Destructors are executed in *reverse order of constructors*

### Overriding
This is a properties inside subclass(derived class)

Function in the derived class with the same function name will override the function in the base class

We can still retrieve the overridden functions by using the scope resolution operator ":::"
Ex: We have Files is a parents class and Download is a child class
So to specify the setting function in 2 class we can write like
Files::setting( ) to choose the former 
Download:setting( ) to choose the latter

### Type of class members
![[Pasted image 20250415134619.png | 400]]

#### Public Inheritance
Public and protected members of the base class 
->become respectively *public and protected* members of the derived class
Look back at the "opt" so if the specifiers is PUBLIC
-> Then the public and protected will remain the same in the derived class

#### Private Inheritance
public and protected members of the base class become **private** members of the derived class
![[Pasted image 20250415135859.png | 300]]

#### Protected Inheritance
public and protected members of the base class become **protected** members of the derived class
![[Pasted image 20250415135932.png | 300]]

**Constructor - Initializers**
```Text
class_name::class_name(param-list) : ctor-initializer { 
	// function body 
}
```
ctor-initializer is used to transfer the parameters to the constructors of the base-class

### Destructors
Destructors are called implicitly starting with the last derived class and moving int he direction of the base class

### Compatibility Between Base and Derived Classes 
➢An object of a derived class can be treated as an *object* of its base class 
➢The reverse is not true

### Nested Class Scope
➢A public or protected base class member that is hidden from the derived class can be accessed using the scope resolution operator “::”
➢**For example: base-class::member** 
➢On the contrary, the base class *cannot access* the members of its derived classes

### Implicit Conversion of Derived Pointers to Base Pointers
➢A base type pointer can point to either a base object or a derived object

```Cpp
// Assume Point3D is derived from Point 
Point3D * cp = new Point3D; 
Point3D *cp1; 
Point * p; 
p = cp; //OK normal case
cp1=p; //Error 
cp1=(Point3D*) p;//OK special case
```

### Casting Base pointers to Derived Pointers
A base pointer cannot be *implicitly* converted to a derived pointer
--> this is in the special case
But in the normal case: A base pointer will be automatically convert 


### Multiple Inheritance
### Virtual Base Classes
Not created to have instances/ objects
It is **a nested inner class whose functions and member variables can be overridden and redefined by subclasses of an outer class**.

We use virtual for solving diamond problem
When a class inherits from multiple classes that share common ancestor, so w/o Virtual -> it may ended up storing duplicate copies of the ancestor's members

