### leetcode [538. 把二叉搜索树转换为累加树](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/)

```cpp
/*
	解法：一定要注意审题。
	二叉搜索树的性质是中序遍历（左-根-右）为从小到大的有序序列。
	这里要计算比当前结点大的节点的和，应该按照 右-根-左 的方式遍历二叉树。
	然后每回把根节点的值加上之前的sum，然后将上一步得到的值赋给sum。
*/
```

```cpp
int sum=0;
TreeNode* convertBST(TreeNode* root) {
    if(!root) return nullptr;
    convertBST(root->right);
    root->val+=sum;
    sum=root->val;
    convertBST(root->left);
    return root;
}
```

