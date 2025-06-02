## 1. Objects
Object-based programming
- View the world as a collection of autonomous, interacting objects
	- Ex: people, animals, plants, buildings, etc.

### 1.1 Real-World objects properties
+ Active, autonomous behaviors
	+ not directly controlled by the outside
		+ So the thing is in C++, we can allow or prohibit the access from the outside variable to access the data inside the class
		+ In C, (assume 'h' is a struct) --> h.x = 5 is acceptable
		+ C++, if we declare it in private -> h.x = 5 might raise error
+ Communicative
	+ Can send/receive "messages" to/from other objects
+ Collaborative
	+ Long-term relationships between objects will arise
+ Nested 
	+ Complex objects have other objects as components(which in turn may have object components...) --> struct in struct (C)
+ Uniquely named/identifiable
+ Creation/ Destruction
	+ May be created and destroyed

A good example for real-world objects **A person**
+ Thinks (most of the time)
+ Communicates with others
+ Collaborates and works with others 
+ Has a name (and a NRIC)
+ Is born/then dies

### 1.2 Virtual objects
Objects that exist in programs only:
+Virtual objects consist of the above features
• Virtual objects are **much more precise** in their names, borders, interactions, etc. 
• Virtual objects are the *basic components* for your ==object oriented program==

Example: 
**A bank account**
+ Has a balance, response to messages for deposits, withdrawals, and balance queries
**Set** : Elements can be added, deleted, and queried

+ Messages have both an effect (causing *internal changes* or *induced messages*) and a return value
+ Users only need to know **external view** of aSet to use it 

> [!note] Those are objects with OOP

Stateless $\neq$ Stateful
### Sets in Non-OOP languages
+ a Set itself is structure
+ Operations on a Set are active but **stateless** functions, they do not remember anything from one call to the next

| Stateful                                                                       | Stateless                                                                                                                                          |
| ------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| An object that **maintains information (state)** across multiple method calls. | An object that does not maintain any internal state — it **only performs operations** based on **input and produces output** without side effects. |
| A bank account object that keeps track of the balance.                         | A math utility class that only has pure functions                                                                                                  |
```python
# Stateful
class BankAccount:
    def __init__(self, initial_balance=0):
        self.balance = initial_balance  # State

    def deposit(self, amount):
        self.balance += amount  # Modifies state

    def get_balance(self):
        return self.balance
# Usage:
account = BankAccount(100)
account.deposit(50)
print(account.get_balance())  # Output: 150

```

```python
# Stateless
class MathUtility:
    @staticmethod
    def add(a, b):
        return a + b

# Usage:
result = MathUtility.add(5, 7)
print(result)  # Output: 12

print(increment())  # Output: 2

```

**There is no encapsulation**
+ Programmer could directly manipulate the data, possibly putting the data in a compromised state

## 2. What are objects?
Booch:
+ Something that 'has state, behavior, and identity'
Martin/Odell:
+ Anything, real or abstract, about which we store data and those methods(operations) that manipulate the data
>[!Definition] Peter Müller
>An **object** is an instance of a class. It can be uniquely identified by its *name* and it defines a *state* which is represented by the values of its attributes at a particular time


### 2.1 Message 
Message is a request to an object to invoke one of its methods
A message therefore contains:
+ Name of the method
+ Arguments of the method
### Interface
+ The operation "name" list open to other objects (other objects can send messages)
+ An object has a function but does not show it to the public, this is useless for the public (private function)
+ In C++, only public functions(belong to the interface) **can be called** by other objects (outsiders) 

## Class
- "Class - a definition of **an implementation** (methods and data structures) shared by a group objects"
- --> from this the compiler then allocate memory for the data inside the class
"Class" - a **template** from which objects may be created. It contains a definition of the state descriptors and methods for the objects

### Meta-class : Class of class
+ Explicit support of meta-classes means that objects, classes and meta-classes are treated uniformly 
+ Classes can be created run-time by explicitly sending a message to a special meta-class
+ Not all OOP languages support meta-class
--> Define a class inside another class
**It is not inheritance**
