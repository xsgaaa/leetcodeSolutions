### leetcode [94. 二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

```cpp
/*
	解法：递归和迭代。
*/
```

```cpp
//迭代计算（要掌握的)
vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        if(!root)   return res;
        stack<TreeNode *>st;
        while(root || !st.empty())
        {
            while(root)
            {//如果根节点不为空，就一直访问根节点的左节点
                st.push(root);
                root=root->left;
            }
            root=st.top();	//弹出根节点
            st.pop();
            res.push_back(root->val);	//访问根节点的值
            root=root->right;			//再访问右节点
        }
        return res;
    }

//递归计算，递归不是主流
vector<int> res;
    void dfs(TreeNode *root)
    {
        if(root==nullptr)
            return;
        dfs(root->left);
        res.push_back(root->val);
        dfs(root->right);
    }
    vector<int> inorderTraversal(TreeNode* root) {
        dfs(root);
        return res;
    }
```

