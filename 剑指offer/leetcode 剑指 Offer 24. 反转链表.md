### leetcode [剑指 Offer 24. 反转链表](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/)

```cpp
ListNode* ReverseList(ListNode* pHead) {
        if(pHead==nullptr)    return nullptr;
        ListNode * p0=nullptr;
        ListNode * p1=pHead;
        ListNode * p2=p1->next;
        while(p1)
        {//p1是当前结点，p0是上一个结点，p2是下一个节点
            p1->next=p0;    //改变当前结点的指向
            p0=p1;          //上一个结点换成当前结点
            p1=p2;    //当前结点转到下一个结点
            if(p1==nullptr)    //如果节点为空，代表p0为最后一个结点
                return p0;
            p2=p1->next;
        }
        return nullptr;
    }
```

