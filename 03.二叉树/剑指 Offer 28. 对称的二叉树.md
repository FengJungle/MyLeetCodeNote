# 剑指 Offer 28. 对称的二叉树

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。但是 [1,2,2,null,3,null,3] 则不是镜像对称的.  

```
bool _isSymmetric(TreeNode* L, TreeNode* R)
{
    if(L == NULL && R == NULL)
    {
        return true;
    }
    if((L == NULL && R != NULL) || (R == NULL && L != NULL) || (L->val != R->val))
    {
        return false;
    }
    return _isSymmetric(L->left, R->right) && _isSymmetric(L->right, R->left);
}
bool isSymmetric(TreeNode* root) {
    if(root == NULL)
    {
        return true;
    }
    
    return _isSymmetric(root->left, root->right);
}
```