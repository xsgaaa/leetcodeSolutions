### leetcode [124. 二叉树中的最大路径和](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)

```cpp
/*	
	解法：深度优先搜索。
	注意：计算左右子树的贡献时，不能为负。而且dfs只能返回一条路径的结果。
*/
```

```cpp
int res=INT_MIN;
    int maxPathSum(TreeNode* root) {
        dfs(root);
        return res;
    }
    private:
    int dfs(TreeNode* root)
    {
        if(root==nullptr)   return 0;
        //计算左右子树对结果的贡献，注意贡献不能为负
        int l=max(dfs(root->left),0);   
        int r=max(dfs(root->right),0);  
        res=max(res,r+l+root->val);  
        //返回的时候，只能返回已一条路径的值，如果返回两条路径，就不符合题意了 
        return max(l,r)+root->val;  
    }
```

