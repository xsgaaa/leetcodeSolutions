### leetcode [57. 插入区间](https://leetcode-cn.com/problems/insert-interval/)

解法：关键是在合适的位置进行插入这个新的区间。插入区间之后，其余的处理和[56. 合并区间](https://leetcode-cn.com/problems/merge-intervals/)做法基本一致。

这里假设当发生重合时进行插入，这个处理方式要记住。

在插入区间之后，因为intervals中剩下的区间的本来就是有序的。判断是否发生重合，然后插入即可。

![image-20200820192649442](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200820192649442.png)

```cpp
 vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        auto & ins=intervals;
        auto & nin=newInterval;
        int i=0;
        vector<vector<int>> ans;
        //这个循环终止时，ins[i][1]>=nin[0];区间重合
        while(i<ins.size() && ins[i][1]<nin[0])
            ans.push_back(ins[i++]);    
        ans.push_back(nin);

        while(i<ins.size())
        {
            auto & v1=ans.back();
            auto & v2=ins[i++];
            if(v2[0]<=v1[1])
            {//必然发生重合
                v1[0]=min(v1[0],v2[0]);
                v1[1]=max(v1[1],v2[1]);
            }
            else
                ans.push_back(v2);
        }
        return ans;
    }
```

