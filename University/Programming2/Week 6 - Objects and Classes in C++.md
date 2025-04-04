
## 1 Definition
Classes Member
+ Data member
+ Function member 
**Member access**
+ We can control which data/ function is allowed to access by outsiders
**Memory allocation**
+ System only allocate memory for *objects* which different data (after it has been initialized)
+ So class -> system only give a reference to it -> not allocate yet
**Object copy : Deep vs Shallow**
ex : string name = "name"
so name is an array -> system allocate name "-->"  "n" "a" "m" "e"

*Shallow Copy* char * p = name; it also allocate the same as above
--> change the pointer from p to name

*Deep copy* `char * q = new char[20]`
strcpy() : copy the how array from name into q --> so it just create a new string 
--> any changes made on this q *will not affect name*

```Cpp
class Student{
	string name;
	string address;
	string getName();
}
Student s1;
```

## Control member access
```Cpp
class Point{
	private:
		int x,y;
	public:
		Point(int xVal = 0, int yVal = 0){
			x = xVal;
			y = yVal;
		}
		int getX(){return x};
		int getY(){return y};
};
```

--> Methods and Function is called interchangeably 
A function has its definition or its prototype within the class definition

*Class member*
A class object contains a copy of the data defined in the class
+ function/methods are shared
+ data are not
![[Pasted image 20250404093021.png | 450]]

Private:
+ So it can only be access inside the class
Protected:
+ So for inheritance -> other classes can used member inside the protected 
+ But not for private
![[Pasted image 20250404093858.png | 400]]
![[Pasted image 20250404094053.png | 400]]

*Friend class* : can access private and protected member of other class
```Cpp
#include <iostream>
class A {
    private:
         int a;
    public:
        A() { a=10; } // constructor -> assign a value for it
        void seta(int value);
        friend class B;    // Friend Class
};
void A::seta(int value) { a=value; } // out-of-line function
class B {
 private:
     int b;
 public:
    void showA(A& x) { // pass by reference - no need actually
    // Since we are not changing the value a from class A
	    std::cout << "A::a=" << x.a;   
	}
};
 int main() {
 A a;    
 B b;
 a.seta(15);
 b.showA(a);
 return 0;
 }
```
--> only works when we include "friend" class inside class A
--> otherwise, it will trigger errors, since outsiders cannot access private data other others

## Inline - Outline functions
*In-line* : functions are defined within the body of the class definition
*Out-of-line* : functions are *declared* within the body of the class definition and *defined* outside --> similar to *Friend class example*
*inline* keyword: define an 
![[Pasted image 20250404100021.png | 400]]
