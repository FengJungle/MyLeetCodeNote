# 剑指 Offer 07. 重建二叉树

输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

例如，给出  
  
前序遍历 preorder = [3,9,20,15,7]  
中序遍历 inorder = [9,3,15,20,7]  
返回如下的二叉树：  

    3    
   / \    
  9  20    
    /  \    
   15   7    

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* makeNode(int rootIndex, vector<int>&preorder, int l, int r, vector<int>&inorder)
    {
        if(l > r)
        {
            return NULL;
        }
        TreeNode* root = new TreeNode(preorder[rootIndex]);
        if(l == r)
        {
            return root;
        }    
        int mid = l;
        while(inorder[mid] != root->val && mid <= r)
        {
            mid++;
        }
        root->left = makeNode(rootIndex+1, preorder, l, mid-1, inorder);
        root->right = makeNode(rootIndex+mid-l+1, preorder, mid+1, r, inorder);
        return root;
    }

    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        TreeNode* root = NULL;
        if(preorder.size() == 0 || inorder.size() == 0)
        {
            return root;
        }
        root = makeNode(0, preorder, 0, inorder.size()-1, inorder);
        return root;
    }
};
```