### Leetcode [128. 最长连续序列](https://leetcode-cn.com/problems/longest-consecutive-sequence/)

解法：由于题目要求了要用`O(1)`的方法，因此要使用哈希。

```cpp
代码1:如果一个数 i 的前一位 i-1 不存在,就对其进行求长度。可以防止因为从连续数字的中间位置求时造成的较高的复杂度。
比如：4 3 2 1。当我们从 3 开始求时，要访问 4 。当我们从 2 开始求时，还要求 3 和 4。
```

```cpp
int longestConsecutive(vector<int>& nums) {
        int N=nums.size();
        unordered_set<int> S;
        for(auto & i:nums)
            S.insert(i);
        int res=0;
        for(auto i:nums)
        {
            if(!S.count(i-1))
            {
                int len=1;
                while(S.count(i+1))
                {
                    i++;
                    len++;
                }
                res=max(res,len);
            }
        }
        return res;
    }
```

```
代码2：记忆化递归
```

```cpp
int longestConsecutive(vector<int>& nums) {
        int N=nums.size();
        unordered_map<int,int> mp;
        for(int i=0;i<N;i++)
        {
            mp[nums[i]]=0;
        }
        int res=0;
        for(int i=0;i<N;i++)
        {
            if(mp[nums[i]]) continue;
            res=max(res,dfs(mp,nums[i]));
        }
        return res;
    }
private:
    int dfs(unordered_map<int,int> & mp,int num)
    {
        if(mp.count(num)==0)    return 0;
        if(mp[num]) return mp[num];
        int ret=dfs(mp,num-1);
        mp[num]=ret+1;
        return mp[num];
    }
```