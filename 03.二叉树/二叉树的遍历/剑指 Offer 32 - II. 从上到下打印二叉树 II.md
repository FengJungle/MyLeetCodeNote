# 剑指 Offer 32 - II. 从上到下打印二叉树 II
从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

##### 例如:
给定二叉树: [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
返回其层次遍历结果：
```
[
  [3],
  [9,20],
  [15,7]
]  
```

### 解法1：层序遍历
```
vector<vector<int>> levelOrder(TreeNode* root) {
    vector<vector<int>>ret;
    if(root == NULL)
    {
        return ret;
    }
    queue<TreeNode*>q;
    q.push(root);
    TreeNode* cur = NULL;
    while(!q.empty())
    {
        int count = q.size();
        vector<int>tmp;
        while(count != 0)
        {
            cur = q.front();
            q.pop();
            tmp.push_back(cur->val);
            count--;
            if(cur->left != NULL)
            {
                q.push(cur->left);
            }
            if(cur->right != NULL)
            {
                q.push(cur->right);
            }
        }
        ret.push_back(tmp);
    }

    return ret;
}
```