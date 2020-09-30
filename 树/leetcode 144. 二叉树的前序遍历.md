### leetcode [144. 二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)

> 给定一个二叉树，返回它的 前序 遍历。
>
>  示例:
>
> 输入: [1,null,2,3]  
>    1
>     \
>      2
>     /
>    3 
>
> 输出: [1,2,3]
> 进阶: 递归算法很简单，你可以通过迭代算法完成吗？

```cpp
//迭代
vector<int> ans;
    vector<int> preorderTraversal(TreeNode* root) {
        if(root==nullptr)
            return ans;
        stack<TreeNode*> st;
        st.push(root);
        while(!st.empty())
        {
            TreeNode* tmp=st.top();st.pop();
            ans.push_back(tmp->val);
            if(tmp->right!=nullptr)
                st.push(tmp->right);
            if(tmp->left!=nullptr)
                st.push(tmp->left);
        }
        return ans;
    }
```

```cpp
//递归
 vector<int> ans;
void dfs(TreeNode* root)
{
    if(root==NULL)
        return;
    ans.push_back(root->val);
    dfs(root->left);
    dfs(root->right);
}
vector<int> preorderTraversal(TreeNode* root) {
    dfs(root);
    return ans;
}
```

