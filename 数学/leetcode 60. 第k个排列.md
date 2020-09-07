### leetcode [60. 第k个排列](https://leetcode-cn.com/problems/permutation-sequence/)

```cpp
/*
	解法;数学。
*/
```

```cpp
//假如n=3,k=3。
//第一轮,num=k%A[3-1]=1,idx=k/A[3-1]=1,num>0,代表只能选择链表中idx索引位置的值2,并将其删除，之后k=1
//第二轮,num=k%A[2-1]=0,idx=1/A[2-1]=1,num=0,代表选择链表中idx-1索引位置的值1，并将其删除。
//由于num=0,之后必然是一个倒序的排列。退出逆序构造一下即可。
list <int> _list;
string getPermutation(int n, int k) {
    int A[n+1];
    A[0]=1;
    for(int i=1;i<=n;i++)   
    {
        A[i]=A[i-1]*i;
        _list.push_back(i); //待选择链表
    }
    string ans;
    int cnt=n;
    while(k>0 && cnt>1)
    {
        int idx=k/A[cnt-1];     //除以(除当前位以外的之后的数的排列的可能)
        int num=k%A[cnt-1];     //计算余数
        if(num>0)
        {
            auto it=next(_list.begin(),idx);
            ans+=to_string(*it);
            _list.erase(it);
            k=num;
        }   
        else
        {
            auto it=next(_list.begin(),idx-1);
            ans+=to_string(*it);
            _list.erase(it);
            break;
        }
        cnt--;
    }
    for(auto it=_list.rbegin();it!=_list.rend();it++)
        ans+=to_string(*it);
    return  ans;
}
```

