## 419. Battleships in a Board

https://leetcode.com/problems/battleships-in-a-board/description/

Given an 2D board, count how many battleships are in it. The battleships are represented with 'X's, empty slots are represented with '.'s. You may assume the following rules:
You receive a valid board, made of only battleships or empty slots.
Battleships can only be placed horizontally or vertically. In other words, they can only be made of the shape 1xN (1 row, N columns) or Nx1 (N rows, 1 column), where N can be of any size.
At least one horizontal or vertical cell separates between two battleships - there are no adjacent battleships.
```
Example:
X..X
...X
...X
In the above board there are 2 battleships.
Invalid Example:
...X
XXXX
...X
This is an invalid board that you will not receive - as battleships will always have a cell separating between them.
```

Solution:
```c++
static string opt =[](){
    std::ios::sync_with_stdio(false);
    cin.tie(NULL);
    return "";
}();

class Solution {
public:
    int countBattleships(vector<vector<char>>& board) {
        int counter = 0;
        for (int i = 0; i < board.size(); ++i) {
            for (int j = 0; j < board[i].size(); ++j) {
                if (board[i][j] == 'X') {
                    if (i > 0) {
                        if (j > 0) {
                            if (board[i - 1][j] == '.' && board[i][j - 1] == '.') {
                                ++counter;
                            }
                        } else {
                            if (board[i - 1][0] == '.') {
                                ++counter;
                            }
                        }
                    } else {
                        if (j > 0) {
                            if (board[0][j - 1] == '.') {
                                ++counter;
                            }
                        } else {
                            ++counter;
                        }
                    }
                }
            }
        }
        return counter;
    }
};
```
