## 442. Find All Duplicates in an Array

https://leetcode.com/problems/find-all-duplicates-in-an-array/description/

Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements that appear twice in this array.

Could you do it without extra space and in O(n) runtime?

```
Example:
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
```

Solution:

```c++
static string opt = [](){
    std::ios::sync_with_stdio(false);
    cin.tie(NULL);
    return "";
}();

class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        vector<int> res;
        
        for (int n: nums) {
            int pos = abs(n);
            if(nums[pos - 1] > 0) {
                nums[pos - 1] *= -1;
            } else {
                res.push_back(pos);
            }
        }
        
        return res;
    }
};
```
