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
• Virtual objects are **much more precise** in their names, borders, interactions, etc. • Virtual objects are the *basic components* for your ==object oriented program==

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