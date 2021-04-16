# 剑指 Offer 47. 礼物的最大价值
在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

##### 示例 1:

输入: 
```
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]  
```
输出: 12  
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物  

### 解法1：动态规划
```
int maxValue(vector<vector<int>>& grid) {
    if(grid.size() == 0 || grid[0].size() == 0)
    {
        return 0;
    }
    int m = grid.size();
    int n = grid[0].size();
    vector<vector<int>>dp(m, vector<int>(n, 0));
    dp[0][0] = grid[0][0];
    for(int row = 1;row < m;row++)
    {
        dp[row][0] = grid[row][0] + dp[row-1][0];
    }
    for(int col = 1;col < n;col++)
    {
        dp[0][col] = grid[0][col] +  dp[0][col-1];
    }
    for(int i = 1;i<m;i++)
    {
        for(int j = 1;j<n;j++)
        {
            dp[i][j] = grid[i][j] + max(dp[i-1][j], dp[i][j-1]);
        }
    }
    return dp[m-1][n-1];
}
```