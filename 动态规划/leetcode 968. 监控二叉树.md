### leetcode [968. 监控二叉树](https://leetcode-cn.com/problems/binary-tree-cameras/)

```cpp
/*
	解法：树形DP。
	树形DP一般是先遍历到底层，然后再从下往上进行回溯，回溯的时候得到结果。
	自底向上进行计算。
*/
```

```cpp
//0 表示不需要监控的状态
    //1 表示待监控的状态
    //2 表示结点进行的监控的状态
    int dfs(TreeNode *root)
    {
        if(root==nullptr)   return 0;
        int left=dfs(root->left);
        int right=dfs(root->right);

        if(left+right==0)
            return 1;
        else if(left==1 || right==1)
        {
            res++;
            return 2;
        }
        else 
            return 0;
    }
    int minCameraCover(TreeNode* root) {
        TreeNode *dumyhead=new TreeNode(-1);
        dumyhead->left=root;
        dfs(dumyhead);
        return res;
    }
private:
    int res=0;
```

