### leetcode [234. 回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)

> 请判断一个链表是否为回文链表。
>
> 示例 1:
>
> 输入: 1->2
> 输出: false
> 示例 2:
>
> 输入: 1->2->2->1
> 输出: true
> 进阶：
> 你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？

```cpp
/*
	解法: Two pointers.
*/
bool isPalindrome(ListNode* head) {
        if(head==nullptr || head->next==nullptr)   return true;
        ListNode *slow=head,*fast=head;
        while(fast->next && fast->next->next)
        {//find the middle point of Linklist
            slow=slow->next;
            fast=fast->next->next;
        }
        ListNode *mid=slow->next,*ne=mid->next;
        mid->next=nullptr;
        while(ne)
        {//reverse the right part of Linklist
            ListNode *nene=ne->next;
            ne->next=mid;
            mid=ne;
            ne=nene;
        }
        slow=head;
        while(mid && slow)
        {//compare the characters
            if(slow->val!=mid->val)
                return false;
            mid=mid->next;
            slow=slow->next;
        }
        return true;
    }
```

