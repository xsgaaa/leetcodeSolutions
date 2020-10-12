### leetcode [530. 二叉搜索树的最小绝对差](https://leetcode-cn.com/problems/minimum-absolute-difference-in-bst/)

> 给你一棵所有节点为非负值的二叉搜索树，请你计算树中任意两节点的差的绝对值的最小值。
>
>  
>
> 示例：
>
> 输入：
>
>    1
>     \
>      3
>     /
>    2
>
> 输出：
> 1
>
> 解释：
> 最小绝对差为 1，其中 2 和 1 的差的绝对值为 1（或者 2 和 3）。

```java
/*
	解法：利用中序遍历的方式。
	记录前一个结点，然后用当前结点减去前一个结点的值，与结果res取最小值即可。
*/
public int res=Integer.MAX_VALUE;
public TreeNode pre=null;
public void dfs(TreeNode root)
{
    if(root==null)  return;
    dfs(root.left);
    if(pre!=null)
        res=Math.min(res,root.val-pre.val);
    pre=root;
    dfs(root.right);
}
public int getMinimumDifference(TreeNode root) {
    dfs(root);
    return res;
}
```

