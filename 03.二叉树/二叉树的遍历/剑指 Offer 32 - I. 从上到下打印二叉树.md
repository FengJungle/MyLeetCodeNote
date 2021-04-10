# 剑指 Offer 32 - I. 从上到下打印二叉树
从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

例如:
给定二叉树: [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
返回：

[3,9,20,15,7]
### 解法1：二叉树的层序遍历
```
vector<int> levelOrder(TreeNode* root) {
    if(root == NULL)
    {
        return vector<int>();
    }
    queue<TreeNode*>q;
    q.push(root);
    TreeNode* cur;
    vector<int>ret;
    while(!q.empty())
    {
        cur = q.front();
        q.pop();
        ret.push_back(cur->val);
        if(cur->left != NULL)
        {
            q.push(cur->left);
        }
        if(cur->right != NULL)
        {
            q.push(cur->right);
        }
    }
    return ret;
}
```