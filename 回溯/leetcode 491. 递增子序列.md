### leetcode [491. 递增子序列](https://leetcode-cn.com/problems/increasing-subsequences/)

```cpp
/*
	解法：dfs+剪枝
	当本次循环的元素小于数组中前一个元素，并且本次选择的元素在本轮已经出现过时，跳过即可
*/
```

```cpp
vector<vector<int>> res;
vector<int> tmpres;
void dfs(int st,int end,vector<int> & nums)
{
    if(tmpres.size()>=2)
    {
        res.push_back(tmpres);
    }
    if(st>=end) return;
    unordered_set<int> S;
    for(int i=st;i<end;i++)
    {
        if(S.count(nums[i]) || (!tmpres.empty() && tmpres.back()> nums[i]))	//剪枝
            continue;
        S.insert(nums[i]);
        if(tmpres.empty()|| nums[i]>=tmpres.back())
        {
            tmpres.push_back(nums[i]);
            dfs(i+1,end,nums);
            tmpres.pop_back();
        }
    }
}
vector<vector<int>> findSubsequences(vector<int>& nums) {
    int N=nums.size();
    dfs(0,N,nums);
    return res;
}
```

