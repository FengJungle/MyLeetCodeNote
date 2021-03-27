# 剑指 Offer 27. 二叉树的镜像

请完成一个函数，输入一个二叉树，该函数输出它的镜像。
  
例如输入：  
  
     4  
   /   \  
  2     7  
 / \   / \  
1   3 6   9  
镜像输出：  
  
     4  
   /   \  
  7     2  
 / \   / \  
9   6 3   1  

##### 示例 1： 
  
输入：root = [4,2,7,1,3,6,9]  
输出：[4,7,2,9,6,3,1]  

### 方法1： 递归
交换每个节点的左右子节点的位置即可，递归调用  

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
    TreeNode* _mirrorTree(TreeNode* root)
    {
        if(root == NULL)
        {
            return NULL;
        }
        TreeNode* tmp = root->left;
        root->left = root->right;
        root->right = tmp;
        _mirrorTree(root->left);
        _mirrorTree(root->right);
        return root;
    }
    TreeNode* mirrorTree(TreeNode* root) {
        return _mirrorTree(root);
    }
};
```
### 方法2：栈
```
class Solution {
public:
    TreeNode* mirrorTree(TreeNode* root) {
        if(root == NULL)
        {
            return NULL;
        }
        stack<TreeNode*>s;
        s.push(root);
        while(!s.empty())
        {
            TreeNode* node = s.top();
            s.pop();
            if(node == NULL)
            {
                continue;
            }
            TreeNode* tmp = node->left;
            node->left = node->right;
            node->right = tmp;
            s.push(node->left);
            s.push(node->right);
        }
        return root;
    }
};
```