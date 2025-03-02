# ==Binary Search==
#binarySearch #binary
#### <u>Method 1 </u>
- Intuitive thought: Resembles looking for a word in a dictionary
	- each step halves the size of active region by half
	- If the middle position is the target --> terminate
	- Otherwise, recursively move left or right with regard to the middle element
Implementing Code:
```C++
// O(logn)
int a = 0, b = n-1; 
while (a <= b) { 
	int k = (a+b)/2; 
	if (array[k] == x) { 
		// x found at index k 
	} 
	if (array[k] > x) b = k - 1; 
	else a = k + 1; 
}
```
#### <u>Method 2</u>
- Make Jumps and slow down when it get closer to THE TARGET
- The search goes from left to right with initial jump is n/2, then n/4, n/8, .... until the length is 1
- After the jump:
	- Target has been found or
	- It does not exist in the array
```C++
int k = 0; 
for (int b = n/2; b >= 1; b /= 2) { 
	while (k+b < n && array[k+b] <= x) 
		k += b; 
} 
if (array[k] == x) { 
	// x found at index k }
}
```
##### Additional C++ functions
<font color="#ff0000">The container has to be SORTED</font>
 ```C++
 std::vector<int> v = {10, 20, 30, 40, 50};
 auto lb = std::lower_bound(v.begin(), v.end(), target); // lowerbound
 auto ub = std::upper_bound(v.begin(), v.end(), target); // upperbound
```
Both act as two iterators ( which is similar to a pointer but it is in the container | vector, array, etc.)
- Former returns a pointer to the value of the first number who is at ==LEAST== the TARGET
- Latter returns a pointer to first element whose value is ==larger== than the TARGET

```C++
v.begin() // return a pointer to the first element of the array
auto it = v.begin();      //Doable - Dereference : *it 
                          //       - Memory address: &(*it)

v.end() // return a pointer to *one past the last element (which is invalid to dereference). Which mean after the last element 
```
Since iterators only return value of the element 
--> To get the index 
```C++
int index = lb - v.begin();  // Gives distance from first element
```
Count number of elements whose value is TARGET : x
```C++
auto a = lower_bound(array, array+n, x); 
auto b = upper_bound(array, array+n, x); 
cout << b-a << "\n";
```
or 
```C++
auto r = equal_range(array, array+n, x); cout << r.second-r.first << "\n";
```
<font color="#ff0000">AGAIN, THE ARRAY MUST BE SORTED</font>

#### APPLICATION OF BINARY SEARCH 
#binarySearch 
##### Find the smallest solution
```C++
int x =-1; 
for (int b = z; b >= 1; b /= 2) { 
	while(!ok(x+b)) 
		x += b; // this will terminate right after the smallest is found 
				// (b will not be added up)
} 
int k = x+1;
```
ok(x) returns true if x >= k and false if x < k   " \ . / "  just like this, the top is k
That means we can find the smallest value as soon as the ok(x) turns true
##### Find the maximum value
* Similarly, we can find the value which first increase then decrease
* Find position k such that 
	* f(x) < f(x+1) when x < k
	* f(x) > f(x+1) when x >= k

```C++
int x =-1; 
for (int b = z; b >= 1; b /= 2) { 
	while (f(x+b) < f(x+b+1))  // similar to above solution 
		x += b; 
} 
int k = x+1;
```
By allowing x to start at "-1", we'll make sure that the desired number will always be found as X always stayed behind first valid value --> not skip in some edge cases![[Pasted image 20250302085640.png]]
# ==Complete Search==
* General method that can be used to solved almost any algorithm problem.
	* Idea : generate all possible solution and choose the most optimal one using brute force ( or count number of solutions)
	* Downside: Time requirement
		* Solution: Greedy algorithm
				-  Dynamic programming
#### Generating Subset
#backtracking #subset #decisionTree 
* Using recursion, decision tree --> as it goes
	* Choose whether to include a number or not 
```C++
void generateSub(int k, vector<int>& nums, vector<vector<int>>& result, vector<int>& subset ){
        // Base condition to add all of the subset
        if(k >= nums.size()){
            result.push_back(subset);
            return;
        } 
        // Choose to include a number  
        subset.push_back(nums[k]);
        // Recursively include number to a subset
        generateSub(k+1, nums ,result, subset);

		// Choose to not include(empty bracket)
        subset.pop_back();
        while (k + 1 < nums.size() && nums[k] == nums[k + 1]) {
            k++; // additional step for duplicate elements
        }
        //Recursively include number to a subset (for those that are not included before)
        generateSub(k+1,nums, result, subset);
    }

    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        std::vector<vector<int>> result;
        std::vector<int> subset;
        sort(nums.begin(), nums.end());
        generateSub(0, nums, result, subset);
        return result;
    }
```
#### Generating Permutation 
```C++
    void findAll(vector<int>& nums, vector<int>& permutation, vector<vector<int>>& result, vector<bool>& usedNum){
        if(nums.size() == permutation.size()){ // base case if a permu == size
            result.push_back(permutation); // --> add a new permu and return
            return;
        }
        for(int i = 0; i < nums.size(); i++){
            if(usedNum[i]) continue; // since array contains INT so 
            usedNum[i] = true;       // Create a bool array to store T/F
            permutation.push_back(nums[i]);
            findAll(nums, permutation, result, usedNum); // recursively add new                                              number to form a new permutation
            permutation.pop_back(); // remove it and convert it to false
            usedNum[i] = false; // so it'll be available on the next iteration
        } // 1 2 3 --> 1 --> 1 3 --> 1 3 2
    }
    vector<vector<int>> permute(vector<int>& nums) {
        vector<int> permutation;
        vector<vector<int>> result;
        vector<bool> usedNum(nums.size(), false);
        findAll(nums,permutation, result, usedNum);
        return result;
    }
```

# ==Back-Tracking==
- It is an algorithm to calculate all of the possible solution, Hence it's not designed for optimization problem | This is similar to Brute-Force
- BOUNDING-FUNCTION : a condition that kill a NODE in a tree 
	- Take permutation as an example but : Boy1, Boy2, Girl1
		- The condition: girl cannot sit in the middle
		- Write a base statement --> that end/abort the node(permutation) if the above requirement is violated
	- This is called ***==BRANCH AND BOUND==***
Backtracking :                DFS: exploring all of the solution
Branch and Bound:        BFS : Go through level to cross-out invalid solution 
#Queen #backtracking 
- Since we are placi
```C++
void search(vector<char>& diag1, vector<char>& diag2, vector<char>& col,    vector<string>& rowStr, vector<vector<string>>& result, int y, int n){
	if(y == n){ // y represent each Queen from Q1 to Qn
		// This check if we reach the placement of a final queen
		result.push_back(rowStr); // add the board to the result (1 solution)
		return;
	}
	for(int x = 0; x < n; x++){
		if(col[x] == 'Q' || diag1[x + y] == 'Q' || diag2[x - y + n - 1] == 'Q') 
			continue; // Bound Condition row/col/diag1/diag2 so that queen cant  
					// attack each other
		col[x] = diag1[x+y] = diag2[x - y + n - 1] = 'Q'; // Place the queen to the condition
		rowStr[y][x] = 'Q'; // add to the board --> y is a row // x is column
		search(diag1, diag2, col, rowStr, result, y + 1, n); // increase the row (which also mean go to the next queen and place it)
		col[x] = diag1[x + y] = diag2[x - y + n - 1] = '.';
		rowStr[y][x] = 'Q';
	}
}
vector<vector<string>> solveNQueens(int n){
	vector<char> diag1(2*n-1, '.');
	vector<char> diag2(2*n-1, '.');
	vector<char> col(n, '.');
	vector<string> rowStr(n, string(n,'.'));
	vector<vector<string>> result;
	search(diag1, diag2, col, rowStr, result, 0, n);
	return result;
}
```