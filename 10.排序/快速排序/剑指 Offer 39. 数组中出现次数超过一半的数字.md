# 剑指 Offer 39. 数组中出现次数超过一半的数字
数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

##### 示例 1:

输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]  
输出: 2  

### 解法1：排序后的中间数字肯定是
排序，如果一个数字出现次数超过一半，那么排序后中间位置的数字肯定就是答案
```
int majorityElement(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    return nums[nums.size()/2];
}
```
### 解法2：快排思想
借助快速排序的partition思想，将nums分为大于k，等于k和小于k的三段，明确的是，我们要求的是位置为mid处的数字。  
所以我们可以比较mid与三段的边界的情况，根据边界情况做进一步处理：
* 1. mid < lt: 继续在[l, lt]之间partition
* 2. mid > gt: 继续在[gt, r]之间partition
* 3. mid > lt && mid < gt:直接返回key

注意：需要使用三路快排，因为用例中比较多重复的元素
```
int partition(vector<int>&nums, int l, int r, int mid)
{
    int v = nums[l];
    int lt = l;
    int gt = r+1;
    int i = l+1;
    while(i<gt)
    {
        if(nums[i] < v)
        {
            swap(nums[i], nums[lt+1]);
            lt++;
            i++;
        }
        else if(nums[i] > v)
        {
            swap(nums[i], nums[gt-1]);
            gt--;
        }
        else
        {
            i++;
        }
    }
    swap(nums[l], nums[lt]);
    lt--;

    if(mid < lt)
    {
        return partition(nums, 0, lt, mid);
    }
    else if(mid > gt)
    {
        return partition(nums, gt, r, mid);
    }
    else
    {
        return nums[mid];
    }
    return gt;
}
int majorityElement(vector<int>& nums) {
    int l = 0;
    int r = nums.size() - 1;
    int mid = l+(r-l)/2;
    int p = partition(nums, 0, nums.size()-1, mid);

    return p;
}
```
### 解法3：摩尔投票
**摩尔投票法**：
设输入数组 nums 的众数为 xx ，数组长度为 nn 。

* 推论一： 若记众数的票数为+1，非众数 的票数为-1 ，则一定有所有数字的 票数和>0 。
* 推论二： 若数组的前a个数字的 票数和 = 0 ,则 数组剩余 (n-a)个数字的 票数和一定仍 >0 ，即后(n−a) 个数字的众数仍为x。

步骤：  
* 初始化： 票数统计 votes = 0 ， 众数 x；
* 循环： 遍历数组 nums 中的每个数字 num ；
* 当 票数 votes 等于 0 ，则假设当前数字 num 是众数；
* 当 num = x 时，票数 votes 自增 1 ；当 num != x 时，票数 votes 自减 1 ；
* 返回值： 返回 x 即可；  
```
int majorityElement(vector<int>& nums) {
    int v = nums[0];
    int vote = 1;
    for(int i = 1;i<nums.size();i++)
    {
        if(vote == 0)
        {
            v = nums[i];
        }
        vote += (v == nums[i]? 1: -1);
    }
    return v;
}
```