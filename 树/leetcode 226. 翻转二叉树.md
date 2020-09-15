### leetcode [226. 翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/)

```cpp
/*
	解法：递归地交换左右子节点。
*/
```

```cpp
TreeNode* invertTree(TreeNode* root) {
        if(!root)   return root;
        TreeNode *left=invertTree(root->left);
        TreeNode *right=invertTree(root->right);
        root->left=right;
        root->right=left;
        return root;
    }
```

