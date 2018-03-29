## 338. Counting Bits

https://leetcode.com/problems/counting-bits/description/

Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

Example:
For num = 5 you should return [0,1,1,2,1,2].

Follow up:

- It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?
- Space complexity should be O(n).
- Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.

Solution:
```c++
static string opt = [](){
    std::ios::sync_with_stdio(false);
    cin.tie(NULL);
    return "";
}();

class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> res(num + 1);
        res[0] = 0;
        res[1] = 1;
        int powOfTwo = 2;
        int prevPowOfTwo = 1;
        while (powOfTwo <= num) {
            int nextPowOfTwo = powOfTwo * 2;
            int middle = (powOfTwo + nextPowOfTwo) / 2;
            for (int i = powOfTwo; i < min(num + 1, middle); ++i) {
                res[i] = res[i - prevPowOfTwo];
            }
            for (int i = middle; i < min(num + 1, nextPowOfTwo); ++i) {
                res[i] = res[i - prevPowOfTwo] + 1;
            }
            prevPowOfTwo = powOfTwo;
            powOfTwo = nextPowOfTwo;
        }
        return res;
    }
};
```
