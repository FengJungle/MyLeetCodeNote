# 剑指 Offer 12. 矩阵中的路径
请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一格开始，每一步可以在矩阵中向左、右、上、下移动一格。如果一条路径经过了矩阵的某一格，那么该路径不能再次进入该格子。例如，在下面的3×4的矩阵中包含一条字符串“bfce”的路径（路径中的字母用加粗标出）。  
[["a","b","c","e"],  
["s","f","c","s"],   
["a","d","e","e"]]  
  
但矩阵中不包含字符串“abfb”的路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入这个格子。  

##### 示例 1：  

输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"  
输出：true  
##### 示例 2：

输入：board = [["a","b"],["c","d"]], word = "abcd"  
输出：false  

提示：  

1 <= board.length <= 200  
1 <= board[i].length <= 200  

### 方法1：回溯法
```
bool hasPath(vector<vector<char>>& board, string word, vector<vector<bool>>& visited, int rows, int cols, int row, int col, int pathLength)
{
    if(pathLength == word.length())
    {
        return true;
    }
    bool b_hasPath = false;
    if(row >= 0 && row<rows &&
    col >= 0 &&  col < cols && 
    visited[row][col] == false && 
    word[pathLength] == board[row][col])
    {
        visited[row][col] = true;
        pathLength++;
        b_hasPath = hasPath(board, word, visited, rows, cols, row+1, col, pathLength)
        || hasPath(board, word, visited, rows, cols, row-1, col, pathLength)
        || hasPath(board, word, visited, rows, cols, row, col+1, pathLength)
        || hasPath(board, word, visited, rows, cols, row, col-1, pathLength);
        if(b_hasPath == false)
        {
            visited[row][col] = false;
            pathLength--;
        }
    }
    return b_hasPath;
}

bool exist(vector<vector<char>>& board, string word) {
    if(board.size() == 0 || board[0].size() == 0 || word.length() == 0)
    {
        return false;
    }
    int rows = board.size();
    int cols = board[0].size();
    vector<vector<bool>>visited(rows, vector<bool>(cols, false));
    int pathLength = 0;
    for(int row = 0; row < rows;row++)
    {
        for(int col = 0;col<cols;col++)
        {
            if(hasPath(board, word, visited, rows, cols, row, col, pathLength) == true)
            {
                return true;
            }
        }
    }
    
    return false;
}
```