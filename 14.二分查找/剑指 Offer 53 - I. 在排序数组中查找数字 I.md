# 剑指 Offer 53 - I. 在排序数组中查找数字 I
统计一个数字在排序数组中出现的次数。

##### 示例 1:

输入: nums = [5,7,7,8,8,10], target = 8  
输出: 2  
##### 示例 2:  

输入: nums = [5,7,7,8,8,10], target = 6  
输出: 0  

### 解法1：
floor二分查找
```
int search(vector<int>& nums, int target) {
    int l = -1;
    int r = nums.size()-1;
    while(l < r)
    {
        int mid = l + (r-l+1)/2;
        if(nums[mid] >= target)
        {
            r = mid-1;
        }
        else
        {
            l = mid;
        }
    }

    int count = 0;
    if(l+1<nums.size() && nums[l+1] == target)
    {
        int i = l+1;
        while( i < nums.size() && nums[i] == target)
        {
            count++;
            i++;
        }
    }
    return count;
}
```