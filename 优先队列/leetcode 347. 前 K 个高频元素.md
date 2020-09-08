### leetcode [347. 前 K 个高频元素](https://leetcode-cn.com/problems/top-k-frequent-elements/)

```cpp
/*
	解法:哈希+优先队列。
*/
```

```cpp
typedef pair<int,int> PII;
    vector<int> topKFrequent(vector<int>& nums, int k) {
        if(nums.empty() || k==0)    return {};
        unordered_map<int,int> mp;
        for(auto &n:nums)
            mp[n]++;						//哈希用于统计频率
        priority_queue<PII> pq;
        for(auto &p:mp)
            pq.push({p.second,p.first});	//将频率和数字置换插入优先队列中
        vector<int> ans;
        while(k--)
        {							
            ans.push_back(pq.top().second);	//保存结果
            pq.pop();
        }

        return ans;
    }
```

