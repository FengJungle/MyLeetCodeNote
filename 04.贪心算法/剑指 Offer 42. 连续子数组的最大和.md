# 剑指 Offer 42. 连续子数组的最大和
输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。  

### 示例1:
  
输入: nums = [-2,1,-3,4,-1,2,1,-5,4]  
输出: 6  
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。  

### 解法1：贪心算法
变量tmpMax保存当前的和，如果当前的和已经小于0，那么还不如从下一个数开始计算，因为下一个数加上当前的负数，只会比下一个数更小！  
当然，用一个变量result来保存最大的子数组的和。
```
int maxSubArray(vector<int>& nums) {
    if(nums.size() == 1)
    {
        return nums[0];
    }
    int result = nums[0];
    int tmpMax = nums[0];
    for(int i = 1;i<nums.size();i++)
    {
        if(tmpMax < 0)
        {
            tmpMax = 0;
        }
        tmpMax += nums[i];
        if(tmpMax > result)
        {
            result = tmpMax;
        }
    }
    return result;
}
```
### 解法2：动态规划
* 1. 数组含义——dp[i]: 表示0~i的序列，最大连续子序列和为dp[i]
* 2. 递推关系：显然，如果当前和还不如nums[i]大的话，那就从nums[i]开始
```
dp[i] = max(nums[i], dp[i-1]+nums[i]); 
```
* 3. 初始化：dp[0] = nums[0]
```
int maxSubArray(vector<int>& nums) {
    vector<int>dp(nums.size(), 0);
    dp[0] = nums[0];
    int result = nums[0];
    for(int i = 1;i<nums.size();i++)
    {
        dp[i] = max(dp[i-1]+nums[i], nums[i]);
        result = max(dp[i], result);
    }
    return result;
}
```