### leetcode [剑指 Offer 36. 二叉搜索树与双向链表](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

> 解法：递归。记录首节点以及前一个结点

```cpp
void dfs(Node*root,Node* &head,Node* &pre)
{//注意这里必须使用引用，否则只传值而无法修改指针
    if(!root)   return;
    dfs(root->left,head,pre);
    if(!head)
    {
        head=root;
        pre=root;
    }
    else
    {
        pre->right=root;
        root->left=pre;
        pre=root;
    }
    dfs(root->right,head,pre);
}
    Node* treeToDoublyList(Node* root) {
        if(!root)   return nullptr;
        Node *head=nullptr,*pre=nullptr;
        dfs(root,head,pre);
        head->left=pre;
        pre->right=head;
        return head;
    }
```

