### leetcode [1365. 有多少小于当前数字的数字](https://leetcode-cn.com/problems/how-many-numbers-are-smaller-than-the-current-number/)

> 给你一个数组 nums，对于其中每个元素 nums[i]，请你统计数组中比它小的所有数字的数目。
>
> 换而言之，对于每个 nums[i] 你必须计算出有效的 j 的数量，其中 j 满足 j != i 且 nums[j] < nums[i] 。
>
> 以数组形式返回答案。
>

```cpp
/*
	解法一:时间复杂度O(NlogN),空间复杂度O(N)
	利用快速排序。
*/
typedef pair<int,int> PII;
vector<int> smallerNumbersThanCurrent(vector<int>& nums) {
    vector<PII> v;
    for(int i=0;i<nums.size();i++)
    {
        v.emplace_back(nums[i],i);
    }
    sort(v.begin(),v.end());
    vector<int> res(nums.size(),0);
    int cur=-1,cnt=0;
    for(int i=0;i<v.size();i++)
    {
        if(cur!=v[i].first)
            cur=v[i].first,cnt=i;
        res[v[i].second]=cnt;     
    }
    return res;
}
/*
	解法二:由于题目中明确给出范围，可以用桶排序。
	代码略。
*/
```

