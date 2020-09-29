### Leetcode [145. 二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)

> 给定一个二叉树，返回它的 后序 遍历。
>
> 示例:
>
> 输入: [1,null,2,3]  
>    1
>     \
>      2
>     /
>    3 
>
> 输出: [3,2,1]
> 进阶: 递归算法很简单，你可以通过迭代算法完成吗

```cpp
//递归
vector<int> res;
    void dfs(TreeNode *root)
    {
        if(root==nullptr)   return;
        dfs(root->left);
        dfs(root->right);
        res.push_back(root->val);
    }
    vector<int> postorderTraversal(TreeNode* root) {
        dfs(root);
        return res;
    }
```

```cpp
//迭代
vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        if(!root)   return res;

        stack<TreeNode*> st;
        TreeNode *pre=nullptr;
        while(root || !st.empty())
        {
            while(root)
            {
                st.push(root);
                root=root->left;
            }
            root=st.top();
            st.pop();
            if(root->right==nullptr || root->right==pre)
            {
                res.emplace_back(root->val);
                pre=root;
                root=nullptr;
            }
            else
            {
                st.emplace(root);
                root=root->right;
            }
        }
        return res;
    }
```

