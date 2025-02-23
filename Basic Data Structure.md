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
## ==Priority Queue==
#heap 
- This is a ***container adapter*** whose first element is either GREATEST or SMALLEST of all elements in the queue, and elements are in non-increasing or non-decreasing order.
- By default, top element is always the GREATEST by default. 
	- Built on top of Heap Data Structure
- Basically, when we push a new element into priority queue, it will sorted in either order.
```C++
//Greatest
priority_queue<int> q; 
q.push(3); 
q.push(5); 
q.push(7); 
q.push(2); 
cout << "Priority Queue: ";
while (!pq.empty()) {
	cout << pq.top() << ' '; // 7 5 3 2 
    pq.pop(); // remove top everytime it printout
}
q.push(6); 
cout << q.top() << "\n"; // 6 
q.pop()
```
To sort in in increasing order --> the queue has to be declared as following
```C++
priority_queue <int, vector<int>, greater<int>> gq;
// if want to declare the same size as an array
int arr[6] = { 10, 2, 4, 8, 6, 9 };
priority_queue<int, vector<int>, greater<int> > gquiz(arr, arr + 6);
```
###### Note: 
Slight differences between pq.emplace() & pq.push()

| Method    | Use case                                                                           |     |
| --------- | ---------------------------------------------------------------------------------- | --- |
| push()    | When u already have an object and just need to insert it                           |     |
| emplace() | When you want to construct the object in place and avoid unnecessary copies/moves. |     |
```C++
#include <queue>
#include <vector>
#include <iostream>
struct Point {
    int x, y;
    Point(int a, int b) : x(a), y(b) { std::cout << "Point constructed\n"; }
};
int main() {
    std::priority_queue<Point, std::vector<Point>, std::greater<Point>> pq;

    pq.push(Point(1, 2)); // Creates a temporary object, then moves it in
    pq.emplace(3, 4);     // Constructs directly inside the priority queue
    return 0;
}
// example of extra copies/moves
std::priority_queue<int> pq;
int x = 5;
pq.push(x);   // Pushes a copy of x
pq.push(10);  // Pushes 10 directly

```
## ==Stack==
LAST IN FIRST OUT (LIFO)
* provides two O(1) time operations: 
	* adding an element to the top,
	* and removing an element from the top. 
- Only possible to access the top element of a stack
```C++
stack<int> s; 
s.push(3); 
s.push(2); 
s.push(5); 
cout << s.top(); // 5 
s.pop();  
cout << s.top(); // 2 can only see 2 when we remove 5 
```

## ==Pair== 
- Different from map
	- Only hold 1 key-pair value 
	- no ordering of elements
	- returning two values from a function
```C++
// The pair container is defined in <utility> header.
// defining a pair
pair<int, char> PAIR1;
PAIR1.first = 100;
PAIR1.second = 'G'; // second part of the pair
cout << PAIR1.first << " ";   // 100
cout << PAIR1.second << endl; // 'G'
// OR
g2 = make_pair(1, 'a');

// Swap contents of one pair with the other pair
pair1.swap(pair2) ; // MUST be of same type
```
##### Method
+ tie() : create a tuple reference to its arguments
	+ To unpack the tuple values into separate variables
```C++
int main()
{
    pair<int, int> pair1 = { 1, 2 };
    int a, b;
    tie(a, b) = pair1;
    cout << a << " " << b << "\n"; // 1, 2

    pair<int, int> pair2 = { 3, 4 };
    tie(a, ignore) = pair2;
    cout << a << " " << b << "\n"; // 3, 2
```
The use of tie is to refer the desired variables(a, b) to hold the value inside the pair1 which is 1, 2
However, with **"ignore"** keyword --> this will neglect the existence of the value at that position
--> Ex: tie(a, ignore) so now b will not available for unpack 
	--> it will then still hold value of 2 instead of 4

***In case of pair of pairs***
<u>Unpacking needs to be explicitly handled</u>
```C++
pair<int, pair<int, char> > pair3 = { 3, { 4, 'a' } };
int x, y;
char z;
// tie(x,y,z) = pair3; Gives compilation error
// tie(x, tie(y,z)) = pair3; Gives compilation error
// Each pair needs to be explicitly handled
tie(x,ignore) = pair3;
tie(y, z) = pair3.second; // this will refer y and z to second value of pair3
cout << x << " " << y << " " << z << "\n"; // 3 4 a
```
## ==Tuple==
