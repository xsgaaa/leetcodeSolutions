### leetcode [剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

```
/*
	解法：直接正序遍历链表，然后将遍历结果反序。
*/
```

```cpp
vector<int> reversePrint(ListNode* head) {
        vector<int> res;
        while(head)
        {
            res.push_back(head->val);
            head=head->next;
        }
        reverse(res.begin(),res.end());
        return res;
    }
```

