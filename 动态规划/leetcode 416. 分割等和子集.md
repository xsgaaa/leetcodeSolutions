### leetcode [416. 分割等和子集](https://leetcode-cn.com/problems/partition-equal-subset-sum/)

> 给定一个只包含正整数的非空数组。是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。
>
> 注意:
>
> 每个数组中的元素不会超过 100
> 数组的大小不会超过 200
> 示例 1:
>
> 输入: [1, 5, 11, 5]
>
> 输出: true
>
> 解释: 数组可以分割成 [1, 5, 5] 和 [11].
>
>
> 示例 2:
>
> 输入: [1, 2, 3, 5]
>
> 输出: false
>
> 解释: 数组不能分割成两个元素和相等的子集
>

```cpp
/*
	解法：动态规划。0-1背包问题
	先计算总值，判断能否被2整除。
	如果可以整除，那么计算除以2之后的结果value。
	由于是在数组中找一个序列的和value,其中每个数可选可不选，故利用0-1背包的解法。
	注意初值dp[0]=1;
*/
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum=0,tmpsum=0;
        for(auto &i:nums)   sum+=i;
        if(sum%2==1)    return false;
        int value=sum/2;
        vector<int> dp(value+1,0);
        dp[0]=1;
        for(int i=0;i<nums.size();i++)
        {
            for(int j=value;j>=nums[i];j--)
                if(dp[j]==0)
                    dp[j]=dp[j-nums[i]];
        }
        return dp[value];
    }
};
```

