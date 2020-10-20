### leetcode [143. 重排链表](https://leetcode-cn.com/problems/reorder-list/)

> 给定一个单链表 L：L0→L1→…→Ln-1→Ln ，
> 将其重新排列后变为： L0→Ln→L1→Ln-1→L2→Ln-2→…
>
> 你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。
>
> 示例 1:
>
> 给定链表 1->2->3->4, 重新排列为 1->4->2->3.
> 示例 2:
>
> 给定链表 1->2->3->4->5, 重新排列为 1->5->2->4->3.
>

```cpp
/*
	解法：先利用vector保存链表节点的值，然后利用双指针重新连接链表即可。
	时间复杂度:O(N),空间复杂度：O(N)
*/
void reorderList(ListNode* head) {
        if(head==nullptr)   return;
        vector<ListNode *> vec;
        ListNode *pNode=head;
        while(pNode)
        {
            vec.push_back(pNode);
            pNode=pNode->next;
        }
        int i=0,j=vec.size()-1;
        while(i<j)
        {
            vec[i]->next=vec[j];
            vec[j--]->next=vec[++i];      
        }
        vec[i]
```

