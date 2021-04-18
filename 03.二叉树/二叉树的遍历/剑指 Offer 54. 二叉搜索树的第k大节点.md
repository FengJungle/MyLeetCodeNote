# 剑指 Offer 54. 二叉搜索树的第k大节点
给定一棵二叉搜索树，请找出其中第k大的节点。

##### 示例 1:

输入: root = [3,1,4,null,2], k = 1
```
   3
  / \
 1   4
  \
   2
```
输出: 4
##### 示例 2:

输入: root = [5,3,6,2,4,null,null,1], k = 3
```
       5
      / \
     3   6
    / \
   2   4
  /
 1
```
输出: 4  
### 解法1：二叉树的中序遍历
```
int kthLargest(TreeNode* root, int k) {
    stack<TreeNode*> s;
    TreeNode* cur = root;
    vector<int> midOrder;
    while(cur != NULL || !s.empty())
    {
        while(cur != NULL)
        {
            s.push(cur);
            cur = cur->left;
        }
        cur = s.top();
        s.pop();
        midOrder.push_back(cur->val);
        cur = cur->right;
    }
    return midOrder[midOrder.size()-k];
}
```