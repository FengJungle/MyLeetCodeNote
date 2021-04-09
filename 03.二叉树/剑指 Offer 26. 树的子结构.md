# 剑指 Offer 26. 树的子结构
输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

##### 示例 1：
  
输入：A = [1,2,3], B = [3,1]  
输出：false  
##### 示例 2：

输入：A = [3,4,5,1,2], B = [4,1]  
输出：true  

### 递归
```
bool DoesAHaveB(TreeNode* A, TreeNode* B)
{
    if(B == NULL)
    {
        return true;
    }
    if(A == NULL)
    {
        return false;
    }
    if(A->val == B->val)
    {
        return DoesAHaveB(A->left, B->left) && DoesAHaveB(A->right, B->right);
    }
    else
    {
        return false;
    }
}
bool isSubStructure(TreeNode* A, TreeNode* B) {
    bool ret = false;
    
    if(A != NULL && B != NULL)
    {
        if(A->val == B->val)
        {
            ret = DoesAHaveB(A, B);
        }
        if(ret == false)
        {
            ret = isSubStructure(A->left, B);
        }
        if(ret == false)
        {
            ret = isSubStructure(A->right, B);
        }
    }

    return ret;
}
```