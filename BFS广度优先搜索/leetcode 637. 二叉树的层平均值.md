### leetcode [637. 二叉树的层平均值](https://leetcode-cn.com/problems/average-of-levels-in-binary-tree/)

```cpp
/*
	解法:层次遍历
*/
```

```cpp
vector<double> averageOfLevels(TreeNode* root) {
        vector<double> res;
        if(root==nullptr)   return res;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty())
        {
            int size=q.size();
            double sum=0;
            for(int i=0;i<size;i++)
            {
                auto cur=q.front();q.pop();
                sum+=cur->val;
                if(cur->left)   q.push(cur->left);
                if(cur->right)   q.push(cur->right);
            }
            res.push_back(sum/size);
        }
        return res;
    }
```

