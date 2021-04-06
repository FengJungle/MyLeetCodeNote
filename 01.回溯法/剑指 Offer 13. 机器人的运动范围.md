# 剑指 Offer 13. 机器人的运动范围
地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？  

##### 示例 1：

输入：m = 2, n = 3, k = 1  
输出：3  
##### 示例 2：

输入：m = 3, n = 1, k = 0  
输出：1   

### 方法1： 回溯法
```
int sum_of_num(int num)
{
    int sum = 0;
    while(num != 0)
    {
        sum += num%10;
        num/=10;
    }
    return sum;
}
int sum_of_pos(int i, int j)
{
    return sum_of_num(i)+sum_of_num(j);
}

int getCount(int m, int n, int i, int j, vector<vector<bool>>&visited, int k)
{
    int count = 0;
    if(i>=0 && i<m && j>=0 && j<n && !visited[i][j] && sum_of_pos(i, j)<=k)
    {
        visited[i][j] = true;
        count =  1
        + getCount(m, n, i+1, j, visited, k)
        + getCount(m, n, i-1, j, visited, k)
        + getCount(m, n, i, j+1, visited, k)
        + getCount(m, n, i, j-1, visited, k);
    }
    return count;
}

int movingCount(int m, int n, int k) {
    if(m == 0 || n == 0)
    {
        return 0;
    }
    if(k == 0)
    {
        return 1;
    }
    vector<vector<bool>>visited(m, vector<bool>(n ,false));
    int count = 0;
    count = getCount(m, n, 0, 0, visited, k);
    return count;
}
```