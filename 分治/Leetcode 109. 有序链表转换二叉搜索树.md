### Leetcode 109. 有序链表转换二叉搜索树

解法1：利用数组将链表中结点的元素存储下来。然后递归二分地构造二叉树

```cpp
TreeNode * dfs(vector<ListNode*> &v,int l,int r)
    {
        if(l>r) return nullptr;
        int m=(l+r)/2;
        TreeNode *root=new TreeNode(v[m]->val);
        root->left=dfs(v,l,m-1);
        root->right=dfs(v,m+1,r);
        return root;
    }
    TreeNode* sortedListToBST(ListNode* head) {
        if(head==nullptr)   return nullptr;
        vector<ListNode*> v;
        ListNode * pNode=head;
        while(pNode)
        {
            v.push_back(pNode);
            pNode=pNode->next;
        }
        return  dfs(v,0,v.size()-1);
    }
```

解法2：利用快慢指针。左闭右开的形式。

```cpp
 TreeNode* sortedListToBST(ListNode* head) {
        return buildTree(head,nullptr);
    }
private:
    TreeNode * buildTree(ListNode *head,ListNode * tail)
    {
        if(head==tail)  return nullptr;
        if(head->next==tail) return new TreeNode(head->val);
        ListNode* slow=head,*fast=head;
        //快慢指针找中点
        while(fast!=tail && fast->next!=tail)
        {
            slow=slow->next;
            fast=fast->next->next;
        }
        
        TreeNode *root=new TreeNode(slow->val);
        root->left=buildTree(head,slow);
        root->right=buildTree(slow->next,tail);
        return root;
    }
```



