# 剑指 Offer 57 - II. 和为s的连续正数序列
输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。  
##### 示例 1：

输入：target = 9  
输出：[[2,3,4],[4,5]]  
##### 示例 2：

输入：target = 15  
输出：[[1,2,3,4,5],[4,5,6],[7,8]]  

### 方法1：双指针
如果是在一个有序数列中，找出和为s的两个数，这比较好求：  
两个指针分别指向数列两端，根据两个指针所指数字的和与目标和的大小，来移动左右指针。  

借助该思路，同样用两个指针small和big，不过这次不能把big放在另一端：
* 如果small~big的和等于s，则将small~big的数列保存；
* 如果small~big的和小于s，则big++；
* 如果small~big的和大于s，则small++；

#### 初始条件：
small = 1, big = 2;
#### 结束条件
small < target/2

```
vector<vector<int>> findContinuousSequence(int target) {
    vector<vector<int>>ret;
    if(target < 3)
    {
        return ret;
    }

    int small = 1;
    int big = 2;
    int mid = (target)/2;
    int sum = small + big;
    while(small <= mid)
    {
        if(sum == target)
        {
            vector<int>tmp;
            for(int i = small;i<=big;i++)
            {
                tmp.push_back(i);
            }
            ret.push_back(tmp);
            sum -= small;
            small++;
        }
        else if(sum > target)
        {
            sum -= small;
            small++;
        }
        else
        {
            big++;
            sum += big;
        }
    }
    return ret;
}
```