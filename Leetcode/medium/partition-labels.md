## 763. Partition Labels

https://leetcode.com/problems/partition-labels/description/

A string S of lowercase letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.
```
Example 1:
Input: S = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
```
Note:

- S will have length in range [1, 500].
- S will consist of lowercase letters ('a' to 'z') only.

Solution:
```c++
class Solution {
public:
    int findMin(int endRange, vector<int> const &startRanges) {
        int index = -1;
        for (int i = 0; i < 26; ++i) {
            if (startRanges[i] == endRange + 1) {
                index = i;
            }
        }
        return index;
    }
    
    vector<int> partitionLabels(string S) {
        vector<int> res;
        vector<int> startRanges(26, 501);
        vector<int> endRanges(26, 501);
        
        for (int i = 0; i < S.length(); ++i) {
            int letterIndex = S[i] - 'a';
            if (startRanges[letterIndex] == 501) {
                startRanges[letterIndex] = i;
            }
            endRanges[letterIndex] = i;
        }
        
        int endRange = -1;
        int startRange = findMin(endRange, startRanges);
        while(startRange != -1) {
            endRange = startRange;
            for (int i = 0; i < 26; ++i) {
                if (startRanges[i] > startRanges[startRange] && 
                    startRanges[i] < endRanges[endRange] && 
                    endRanges[i] > endRanges[endRange]) {
                    endRange = i;
                    i = 0;
                }
            }
            res.push_back(endRanges[endRange] - startRanges[startRange] + 1);
            startRange = findMin(endRanges[endRange], startRanges);
        }
        return res;
    }
```
