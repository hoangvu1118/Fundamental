## Custom Comparator
> Often used with sorting algorithms, priority queues, or ordered containers like std::set, std::map

* It returns a bool value 
	* True / False

### Method 1
**==Use as a Function==**
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

## Method 2
__Use as Lambda__
#LargestNumber
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

