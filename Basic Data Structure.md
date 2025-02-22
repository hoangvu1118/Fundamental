### Dynamic Arrays 
#vector #array
* Size can be changed 
```C++
// Add elements
vector<int> v; 
v.push_back(3); // [3] 
v.push_back(2); // [3,2]

// Access elements
cout << v[0] << "\n"; // 3 
cout << v[1] << "\n"; // 2

// Access size
v.size()
for (auto x : v) { // Shorter way to iterate through a vector
	cout << x << "\n"; 
}

// Accessing last element
cout << v.back() << "\n"; // 2
v.pop_back(); // remove the last element
```
**How to initialize a vector** 
```C++
vector<int> v = {2,4,2,5,1};

vector<int> v(10); // size 10, initial value 0 
vector<int> v(10,5); // size 10, initial value 5
```

## String
#string
```C++
string a = "hatti"; 
string b = a+a; // String can be combined using "+" | only if it is STRING
cout << b << "\n"; // hattihatti 
b[5] = ’v’; 
cout << b << "\n"; // hattivatti 
string c = b.substr(3,4); // starts at index 3 --> then spread to the next 4 chars
cout << c << "\n"; // tiva
```

## Set structures
#set 
- Basic operations: Insertion, Search, Removal
	- set : O(logn) time --> based on balanced binary tree
	- unordered_set: O(1) time --> uses hashing