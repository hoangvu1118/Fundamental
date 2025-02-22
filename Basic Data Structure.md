### ==Dynamic Arrays== 
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

## ==String==
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

## ==Set structures==
#set 
- Basic operations: Insertion, Search, Removal
	- set : O(logn) time --> based on balanced binary tree
	- unordered_set: O(1) time --> uses hashing
	- Store unique element so "Count" will result either 1 or 0
```C++
set<int> s; 
s.insert(3);                         // Add a number into the set
s.insert(2);
cout << s.count(3) << "\n"; // 1       Number of occurrance
cout << s.count(4) << "\n"; // 0
s.erase(3);                         // erase the element from the set
s.insert(4); 
cout << s.count(3) << "\n"; // 0 
cout << s.count(4) << "\n"; // 1
```
Iterate through a set
```C++
set<int> s = {2,5,6,8}; 
cout << s.size() << "\n"; // 4 
for (auto x : s) { 
	cout << x << "\n"; 
}
```

<font color="#ff0000">To contain multiple instances of a number --> multiset</font>
```C++
multiset<int> s; 
s.insert(5); 
s.insert(5);
s.insert(5); 
cout << s.count(5) << "\n"; // 3

// When using erase in multiset --> erase all of that number
s.erase(5); 
cout << s.count(5) << "\n"; // 0

// below is how to remove ONLY 1 instance from the set
s.erase(s.find(5)); 
cout << s.count(5) << "\n"; // 2
```
#### Set iterator
Create a pointer that points to the smallest element in the set
	**
## ==Map Structure==
#map 
* Similar to #set which have 2 implementations
* map : O(logn)
* unordered_map: O(1)
```C++
map<string, int> m; 
m["monkey"] = 4; 
m["banana"] = 3; 
m["harpsichord"] = 9; 
cout << m["banana"] << "\n"; // 3
```
If value of a key is requested but MAP does not contain that --> automatically add a new key-value pair, set to 0
```C++
map<string, int> m; 
cout << m["aybabtu"] << "\n"; // 0
```
To check if a key ==EXISTS== in a map
``` C++
if (m.count("aybabtu")) { 
	// key exists 
}
// Print all the key-value pair in the map
for (auto x : m) { 
	cout << x.first << " " << x.second << "\n"; 
}
```
