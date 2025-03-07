## Custom Comparator
#LargestNumber
> Often used with sorting algorithms, priority queues, or ordered containers like std::set, std::map
* It returns a bool value 
	* True / False
#### Method 1
**Use as a Function**
#comparison 
```C++
#include <iostream>
#include <vector>
#include <algorithm>
// Custom comparator function (Descending Order)
bool customCompare(int a, int b) {
    return a > b;  // Sort in descending order
}
int main() {
    std::vector<int> v = {5, 2, 8, 1, 3};
    
    // Sort using custom comparator
    std::sort(v.begin(), v.end(), customCompare); // THING TO REMEMBER
    // Print result
    for (int num : v) {
        std::cout << num << " ";
    }
    return 0;
}
```
#### Method 2
__Use as Lambda__
#lambda
```C++
string largestNumber(vector<int>& nums) {
        std::vector<std::string> bank;
        for(auto str : nums){
            bank.push_back(to_string(str));
        }

        std::sort(begin(bank), end(bank), [](string &a, string &b){ // Lambda

            return a+b > b+a;});

        std::string result;

        if(bank[0] == "0") return "0";

        for(string& numString : bank){

            result += numString;

        }
        return result;
    }
```


## Monotonic Stack
 - It is in either increasing or decreasing order
```C
// [73,74,75,71,69,72,76,73]
int* dailyTemperatures(int* temperatures, int temperaturesSize, int* returnSize) {
    *returnSize = temperaturesSize;
    int *result = (int*)calloc(temperaturesSize, sizeof(int));
    int *stack = (int*)malloc(temperaturesSize *sizeof(int));
    int top = -1;
    for(int i = 0; i < temperaturesSize; i++){
        while(top >= 0 && temperatures[i] > temperatures[stack[top]]){
            int index = stack[top--]; // pop the top
            result[index] = i - index; // calculate the index
        }
        stack[++top] = i;
    }
    free(stack);
    return result;
}
```
Explanation:
First create a result array to store the day difference between warmer day [ . . . . . . . . ]
Second, Create a stack to store the day

It gonna initialize the top to be -1 so that when we start to push value onto the stack
it can start with 0 and repeatedly doing so for the following days

Ex: 73 is pushed on top, then top = 0
--> go to the while since top > 0 and 74 > 73
	--> pop the stack and retrieve the index of "73" since we push the index onto the stack
		--> write into the returnArray the number of day difference which is 1
==> Continue to 75

It's gonna push the day so that the order is follow the decreasing order 
75 71 69 and then 72 
--> It then pop the top at 69 --> which give the result array become [1, 1 ,    ,    , 1,   ,   ,   ]
The first 2 empty space is for 75 and 72 the other is still under calculation
