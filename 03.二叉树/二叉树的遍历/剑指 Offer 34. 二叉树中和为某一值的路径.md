# 剑指 Offer 34. 二叉树中和为某一值的路径
输入一棵二叉树和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。从树的根节点开始往下一直到叶节点所经过的节点形成一条路径。

##### 示例:
给定如下二叉树，以及目标和 target = 22，
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```
返回:  
  
[  
   [5,4,11,2],  
   [5,8,4,5]  
]  

### 解法1：回溯法
- 注意题目要求：必须从根节点出发，必须到达叶子节点
```
vector<vector<int>>ret;
void backtracking(TreeNode* node, int curTarget, vector<int>&path)
{
    if(node == nullptr)
    {
        return;
    }
    curTarget-=node->val;
    path.push_back(node->val);
    if(curTarget == 0 && node->left == nullptr && node->right == nullptr)
    {
        ret.push_back(path);
    }
    else
    {
        backtracking(node->left, curTarget, path);    
        backtracking(node->right, curTarget, path);
    }
    path.pop_back();
}

vector<vector<int>> pathSum(TreeNode* root, int target) {
    vector<int>path;
    if(root == nullptr)
    {
        return ret;
    }
    backtracking(root, target, path);

    return ret;
}
```