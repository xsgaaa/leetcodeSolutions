### leetcode  [257. 二叉树的所有路径](https://leetcode-cn.com/problems/binary-tree-paths/)

```cpp
/*
	解法：DFS。
	注意叶子节点构成的条件，只有root->left 和root->right 都为空才是叶子节点。
*/
```



```
vector<int> v;
    vector<string> ans;
    void dfs(TreeNode *root)
    {
        v.push_back(root->val);
        if(!root->left && !root->right)
        {
            string s;
            s+=to_string(v[0]);
            for(int i=1;i<v.size();i++)
                s+="->"+to_string(v[i]);
            ans.push_back(s);
        }
        if(root->left)
            dfs(root->left);
        if(root->right)
            dfs(root->right);
        v.pop_back();
    }
    vector<string> binaryTreePaths(TreeNode* root) {
        if(root==nullptr)   return ans;
        dfs(root);
        return ans;
    }
```

