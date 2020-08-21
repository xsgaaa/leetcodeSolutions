### leetcode [56. 合并区间](https://leetcode-cn.com/problems/merge-intervals/)

解法：区间合并模板题。首先要保证区间有序，然后从前往后进行合并就行。

```cpp
static bool cmp(vector<int> & v1,vector<int> &v2)
    {
        return v1[0]<v2[0];
    }
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        auto & ins=intervals;
        if(ins.size()==0 || ins.size()==1)  return ins;	//注意!!!
        sort(ins.begin(),ins.end(),cmp);
        vector<vector<int>> res;
        res.push_back(ins[0]);
        for(int i=1;i<ins.size();i++)
        {
            if(ins[i][0]<=res.back()[1])
            {
                res.back()[1]=max(res.back()[1],ins[i][1]);
            }
            else res.push_back(ins[i]);
        }
        return res;
    }
```

