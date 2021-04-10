# 剑指 Offer 33. 二叉搜索树的后序遍历序列
输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 true，否则返回 false。假设输入的数组的任意两个数字都互不相同。

##### 示例 1：

输入: [1,6,3,2,5]  
输出: false  
##### 示例 2：

输入: [1,3,2,6,5]  
输出: true  

### 
```
bool judgePostOrder(vector<int>& postorder, int left, int right)
{
    if(left >= right)
    {
        return true;
    }
    int mid = left;
    int root = right;
    right--;

    while(postorder[mid] < postorder[root])
    {
        mid++;
    }
    for(int i = mid;i<=right;i++)
    {
        if(postorder[i] < postorder[root])
        {
            return false;
        }
    }
    return judgePostOrder(postorder, left, mid-1) && judgePostOrder(postorder, mid, right);
}

bool verifyPostorder(vector<int>& postorder) {
    return judgePostOrder(postorder, 0, postorder.size()-1);
}
```