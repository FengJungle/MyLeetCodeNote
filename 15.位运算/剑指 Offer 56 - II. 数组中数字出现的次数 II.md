# 剑指 Offer 56 - II. 数组中数字出现的次数 II
在一个数组 nums 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

##### 示例 1：

输入：nums = [3,4,3,3]  
输出：4
##### 示例 2：

输入：nums = [9,1,7,9,7,9,7]  
输出：1  
   
##### 限制：
* 1 <= nums.length <= 10000  
* 1 <= nums[i] < 2^31  

### 解法1： 位运算
如果一组元素中，**某个数字出现了三次，那么该数字对应的比特位为1的次数一定是3的倍数**。统计每个比特位出现1的次数，如果某一位出现次数不是3的倍数，说明是只出现一次的元素对应某个bit位。把所有这样的比特位找出来求和，即为所求。

需要注意的是，题目限制了每个数均小于2的31次方，那么一个4字节的整型变量即可满足此范围。
```
int singleNumber(vector<int>& nums) {
    int result = 0;
    int bit[32] = {0};
    for(int i = 0;i<nums.size();i++)
    {
        int cur = nums[i];
        unsigned int bitMask = 1;
        // 低位放在31，否则后面result移位的时候会越界
        for(int j = 31;j>=0;j--)
        {
            if((cur&bitMask) != 0)
            {
                bit[j]++;
            }
            bitMask = bitMask<<1;
        }
    }
    for(int i = 0;i<32;i++)
    {
        result <<= 1;
        result += bit[i]%3;
    }
    return result;
}
```
### 解法2：哈希表
显然可以使用unordered_multiset，一次遍历统计各个元素出现的参数，再遍历哈希表，查找出现次数为1的元素。

### 解法3：暴力