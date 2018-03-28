## 797. All Paths From Source to Target

https://leetcode.com/problems/all-paths-from-source-to-target/description/

Given a directed, acyclic graph of N nodes.  Find all possible paths from node 0 to node N-1, and return them in any order.

The graph is given as follows:  the nodes are 0, 1, ..., graph.length - 1.  graph[i] is a list of all nodes j for which the edge (i, j) exists.

```
Example:
Input: [[1,2], [3], [3], []] 
Output: [[0,1,3],[0,2,3]] 
Explanation: The graph looks like this:
0--->1
|    |
v    v
2--->3
There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
```
Note:

- The number of nodes in the graph will be in the range [2, 15].
- You can print different paths in any order, but you should keep the order of nodes inside one path.

Solution

```c++
class Solution {
public:
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
        vector<vector<int>> res;
        int nodeCount = graph.size();
        queue<pair<int, int>> nodesToVisit;
        vector<int> originPath = {0};
        res.push_back(originPath);
        nodesToVisit.push(make_pair(0, 0));
        while(!nodesToVisit.empty()) {
            for (int i = 0; i < graph[nodesToVisit.front().first].size(); ++i) {
                if (i == graph[nodesToVisit.front().first].size() - 1) {
                    res[nodesToVisit.front().second].push_back(graph[nodesToVisit.front().first][i]);
                    nodesToVisit.push(make_pair(graph[nodesToVisit.front().first][i], nodesToVisit.front().second));
                } else {
                    res.push_back(res[nodesToVisit.front().second]);
                    res[res.size() - 1].push_back(graph[nodesToVisit.front().first][i]);
                    nodesToVisit.push(make_pair(graph[nodesToVisit.front().first][i], res.size() - 1));
                }
            }
            nodesToVisit.pop();
        }
        return res;
    }
};
```
