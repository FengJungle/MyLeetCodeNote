# 剑指 Offer 51. 数组中的逆序对
在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

##### 示例 1:

输入: [7,5,6,4]  
输出: 5  

### 解法1：归并排序
对于两个**已排序**子数组nums1和nums2, 如果nums1中的某个位置i的元素nums1[i] > nums2[j]， 那么数组nums1中i之后的元素肯定也都大于nums2[j]。  归并过程中，按从小到大merge的过程时，只选择当前子序列里的较小值，然后递增索引值。

```
int count = 0;

void merge(vector<int>& nums, int l, int mid, int r)
{
    int* aux = new int[r-l+1];
    for(int k = l;k <= r; k++)
    {
        aux[k-l] = nums[k];
    }   
    int i = l;
    int j = mid+1;
    for(int k = l;k<=r;k++)
    {
        if(i > mid)
        {
            nums[k] = aux[j-l];
            j++;
        }
        else if(j > r)
        {
            nums[k] = aux[i-l];
            i++;
        }
        else if(aux[i-l] <= aux[j-l])
        {
            nums[k] = aux[i-l];
            i++;
        }
        else
        {
            nums[k] = aux[j-l];
            count += mid-i+1;
            j++;
        }
    }

    delete []aux;
}

void mergeSort(vector<int>& nums, int l, int r)
{
    if(l >= r)
    {
        return;
    }
    int mid = l+(r-l)/2;
    mergeSort(nums, l, mid);
    mergeSort(nums, mid+1, r);
    merge(nums, l, mid, r);
}
int reversePairs(vector<int>& nums) {
    mergeSort(nums, 0, nums.size()-1);
    return count;
}
```