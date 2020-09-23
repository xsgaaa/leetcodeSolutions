### [JZ 14 链表中倒数第k个节点](https://www.nowcoder.com/practice/529d3ae5a407492994ad2a246518148a?tpId=13&&tqId=11167&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

> 题目描述
> 输入一个链表，输出该链表中倒数第k个结点。

```cpp
//利用快慢指针，快指针先走k步，然后快慢指针再同时走。
//当快指针走到结尾的时候，慢指针的值即为所求。
/*
struct ListNode {
	int val;
	struct ListNode *next;
	ListNode(int x) :
			val(x), next(NULL) {
	}
};*/
class Solution {
public:
    ListNode* FindKthToTail(ListNode* pListHead, unsigned int k) {
        if(pListHead==nullptr)    return nullptr;
        ListNode* fast=pListHead,*slow=pListHead;
        int cnt=k;
        while(fast && cnt--)
        {
            fast=fast->next;
        }
        while(fast)
        {
            fast=fast->next;
            slow=slow->next;
        }
        if(cnt>0)    return nullptr;
        return slow;
    }
};
```

