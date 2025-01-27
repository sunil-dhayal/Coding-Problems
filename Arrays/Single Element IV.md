# Problem statement

Given an integer array nums, in which exactly two elements appear only once and all the other elements appear exactly three times.
Find the two elements that appear only once. You can return the answer in any order.
You must write an algorithm that runs in linear runtime complexity and uses only constant extra space.

# Solution Hints
The solution is inspired by the solutions to following problems on Leetcode.
  1. [Single Element](https://leetcode.com/problems/single-number/description/)
  2. [Single Element II](https://leetcode.com/problems/single-number-ii/description/)
  3. [Single Elemeent III](https://leetcode.com/problems/single-number-iii/description/) 

# Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        int ones = 0;
        int twos = 0;
        for(int num: nums) {
            ones = (ones ^ num) & (~twos);
            twos = (twos ^ num) & (~ones);
        }
        int xored_1 = 0;
        while(ones){
            if(ones >> xored_1 & 1)
                break;
            xored_1++;
        }
        int value1 = 0, value2 = 0, value3 = 0, value4 = 0;
        for(int num: nums){
            if(num >> xored_1 & 1){
                value1 = (value1 ^ num) & (~value2);
                value2 = (value2 ^ num) & (~value1);
            }
            else {
                value3 = (value3 ^ num) & (~value4);
                value4 = (value4 ^ num) & (~value3);
            }
        }
        return {value1, value3};
    }
};

int main() {
    vector<int> nums = {1,1,1,2,2,2,3,5};
    Solution st;
    vector<int> res = st.singleNumber(nums);
    for(int num: res)
        cout << num<< " ";
}
```
