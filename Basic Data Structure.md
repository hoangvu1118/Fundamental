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
```C++
set<int>::iterator it = s.begin()
// OR
auto it = s.begin()
cout << *it; // dereference to get the value 

// Move iterators like pointers
for (auto it = s.begin(); it != s.end(); it++) { // increase the index it++
	cout << *it << "\n"; // printing in increasing order
} // the same for reverse order
```
#search
```C++
auto it = s.find(x); // find(x) returns an iterator pointing to element (x)
if (it == s.end()) { // if not found --> iterator will be end
	// x is not found 
}
```
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

## ==Deque== 
* Just how it works not including code implementation yet
<font color="#ff0000">- It is dynamic array whose size can be changed at both ends</font>
- Similar to vector with: push_back & pop_back
	- Additionally: push_front & pop_front

> Deque is slower than vector SINCE internal implementation is more complex
```C++
deque<int> d; 
d.push_back(5); // [5]  insert at tail/ rear
d.push_back(2); // [5,2]  insert at tail /rear
d.push_front(3); // [3,5,2]  insert at head/ front
d.pop_back(); // [3,5] delete end
d.pop_front(); // [5]
```
Still, both adding and removing elements take O(1) time on average at both ends.
## ==Queue==
- <font color="#ff0000">FIFO ( First in - First out)</font> 
- Provide two O(1) operations: + Adding to the end of queue
	                       + Removing the front of the queue
- Only possible to access first and last element
<u>Differences from Deque </u>
+ Queue can only be added at the END
+ removed at the front whereas deque can do both operations at both sides of the array
```C++
queue<int> q; 
q.push(3); 
q.push(2); 
q.push(5); 
cout << q.front(); // 3 
q.pop(); 
cout << q.front(); // 2 after remove 3 from the front
```
## Priority Queue

## Stack
* provides two O(1) time operations: 
	* adding an element to the top,
	* and removing an element from the top. 
- Only possible to access the top element of a stack
```C++
```