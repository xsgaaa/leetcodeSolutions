### leetcode [99. 恢复二叉搜索树](https://leetcode-cn.com/problems/recover-binary-search-tree/)

```cpp
/*
	解法：深度优先搜索。
	根据二叉搜索树中序遍历升序的性质进行解题。
	交换两个结点之后，必然不在单调上升。
	如果第一次 出现当前结点小于之前一个结点的情况，记录前一个结点。
	之后出现 重复情况的时候，记录当前结点即可。
*/
```



```cpp
TreeNode *first=nullptr,*second=nullptr;
    TreeNode *pre=new TreeNode(INT_MIN);
    void dfs(TreeNode* root)
    {
        if(root==nullptr)   return;
        dfs(root->left);
        if(root->val<pre->val && !first) first=pre;
        if(root->val<pre->val && first) second=root;
        pre=root;
        dfs(root->right);
    }
    void recoverTree(TreeNode* root) {
        if(root==nullptr)   return;
        dfs(root);
        swap(first->val,second->val);
        return;
    }
```

