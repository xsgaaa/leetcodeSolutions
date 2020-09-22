### leetcode [剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

```cpp
/*
	顺序遍历前序遍历的每个元素，用这个元素来确定左右子树。
*/
```

```cpp
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int idx=0;
    TreeNode * rebuiltTree(vector<int> &pre,vector<int> &vin,int l,int r)
    {
        if(l>r)    return nullptr;
        int i=l;
        for(;i<=r;i++)
        {
            if(vin[i]==pre[idx])
            {
                idx++;
                break;
            }
        }
        TreeNode *root=new TreeNode(vin[i]);
        TreeNode *left=rebuiltTree(pre, vin, l, i-1);
        TreeNode *right=rebuiltTree(pre, vin, i+1, r);
        
        root->left=left;
        root->right=right;
        return root;
    }
    TreeNode* reConstructBinaryTree(vector<int> pre,vector<int> vin) {
        int N=pre.size();
        return rebuiltTree(pre, vin, 0, N-1);
    }
};
```

