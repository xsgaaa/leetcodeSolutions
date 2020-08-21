### leetcode [111. 二叉树的最小深度](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)

解法:递归。**注意题目所说的是到叶子节点的最小深度。**如下图的，最小深度就是2，为根节点到2号结点的深度。

![image-20200821080832514](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200821080832514.png)

```cpp
 int minDepth(TreeNode* root) {
        if(root==nullptr)   return 0;
        int left=minDepth(root->left);
        int right=minDepth(root->right);

        if(root->left==nullptr || root->right==nullptr)
        {//说明当前结点肯定不是叶子节点，计算不为空的子树的高度
            return left==0?right+1:left+1;
        }
        else
            return min(left,right)+1;   //返回最小的
    }
```

