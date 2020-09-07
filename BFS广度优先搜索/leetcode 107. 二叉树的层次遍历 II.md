### leetcode [107. 二叉树的层次遍历 II](https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii/)

```cpp
/*
	解法：BFS层次遍历。
*/
```

```cpp
vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>> res;
        if(root==nullptr)   return res;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty())
        {
            int size=q.size();
            vector<int> tmpres;
            for(int i=0;i<size;i++)
            {
                auto cur=q.front();q.pop();
                tmpres.push_back(cur->val);
                if(cur->left)
                    q.push(cur->left);
                if(cur->right)
                    q.push(cur->right);
            }
            res.push_back(tmpres);
        }
        reverse(res.begin(),res.end());
        return res;
    }
```

