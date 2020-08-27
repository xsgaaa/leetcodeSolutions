### leetcode [632. 最小区间](https://leetcode-cn.com/problems/smallest-range-covering-elements-from-k-lists/)

```cpp
/*
	解法：滑动窗口。
	题目的要求就是在找一个最小的区间，然后区间内，每一个列表都必须有一个数据存在于该区间。
	直观想法是，将列表中所有的元素进行排序，然后用一个滑动窗口，将满足条件的数据全部都包含在窗口中，然后计算窗口的大小。
	和76题是一个道理。
/*
```

```cpp
vector<int> smallestRange(vector<vector<int>>& nums) {
        vector<pair<int,int>> vec;
        for(int i=0;i<nums.size();i++)
        {
            for(int n:nums[i])
                vec.push_back({n,i});
        }
        sort(vec.begin(),vec.end());
        int l=0,r=0;//双指针
        unordered_map<int,int> mp;      //哈希
        vector<int> res={vec[0].first,vec[0].first};
        int cnt=0,dist=INT_MAX;
        while(r<vec.size())
        {
            if(!mp[vec[r].second]++)
                cnt++;
            while(cnt==nums.size())
            {
                if((vec[r].first-vec[l].first)<dist)
                {
                    dist=vec[r].first-vec[l].first;
                    res[0]=vec[l].first;
                    res[1]=vec[r].first;
                }
                if(!--mp[vec[l].second])
                    cnt--;
                l++;                
            }
            r++;
        }
        return res;
    }
```

