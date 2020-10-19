### leetcode [116. 填充每个节点的下一个右侧节点指针](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/)

> 给定一个完美二叉树，其所有叶子节点都在同一层，每个父节点都有两个子节点。二叉树定义如下：
>
> struct Node {
>   int val;
>   Node *left;
>   Node *right;
>   Node *next;
> }
> 填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 NULL。
>
> 初始状态下，所有 next 指针都被设置为 NULL。
>

```java
/*
	解法：用当前层来确定下一层节点的next指针。
*/

public Node connect(Node root) {
        //用当前层去确定下一层的next指针
        if(root==null)   return root;
        Node leftmost=root;
        while(leftmost.left!=null)  //如果下一层的最左边为空，则终止循环
        {
            Node head=leftmost;     //获取当前层的最左边节点
            while(head!=null)       
            {
                head.left.next=head.right;  //当前结点的左节点的下一个节点为其右节点
                if(head.next!=null)
                    head.right.next=head.next.left; //当前结点的右节点的下一个节点为其下一个节点的右节点

                head=head.next;     //节点向右移动
            }
            leftmost=leftmost.left; //获取最左层的节点
        }
        return root;
    }
```

