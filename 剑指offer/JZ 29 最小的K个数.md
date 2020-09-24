### [JZ 29 最小的K个数](https://www.nowcoder.com/practice/6a296eb82cf844ca8539b57c23e6e9bf?tpId=13&&tqId=11182&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

> ## 题目描述
>
> 输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4。

```cpp
 //最小K个数用大顶堆，最大K个数用小顶堆
<int> GetLeastNumbers_Solution(vector<int> input, int k) {
        vector<int> res;
        if(input.empty() || k<=0 || k>input.size())    return res;
        priority_queue<int> pq;
        for(int &num:input)
        {
            if(pq.size()<k)    pq.push(num);
            else if(pq.size()==k)
            {
                if(num<pq.top())
                {
                    pq.pop();
                    pq.push(num);
                }
            }
        }
        
        while(!pq.empty())
        {
            res.push_back(pq.top());
            pq.pop();
        }
        return res;
     }
```

