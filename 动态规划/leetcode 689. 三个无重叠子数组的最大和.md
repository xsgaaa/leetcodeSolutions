### leetcode [689. 三个无重叠子数组的最大和](https://leetcode-cn.com/problems/maximum-sum-of-3-non-overlapping-subarrays/)

```
解法：这题看着挺吓人的，其实不难。首先计算连续k个数的和。
这里，我令sum[i]等于区间[i,i+k-1]的和。
然后问题就变成了取三个数，这三个数的最小相隔k个单位。这个和打家劫舍一个道理的。用动态规划来做。
```

```cpp
vector<int> maxSumOfThreeSubarrays(vector<int>& nums, int k) {
        int N=nums.size();
        vector<int> sum(N-k+1,0);//sum[i]代表以[i,i+k-1]区间内的和
        int num=0;
        for(int i=0;i<k;i++)
        {//首次计算前k个
            num+=nums[i];
        }
        sum[0]=num;
        for(int i=1;i<=N-k;i++)
        {//移动滑窗
            num=num-nums[i-1]+nums[i+k-1];
            sum[i]=num;
        }
        int dp[N-k+2][3];       //定义dp数组
        int plan[N-k+2][3];     //定义方案数组
        memset(dp,0,sizeof dp);
        memset(plan,0,sizeof plan);
        for(int i=1;i<=N-k+1;i++)
        {
            for(int j=0;j<3;j++)
            {
                dp[i][0]=max(dp[i-1][0],sum[i-1]);
                //状态转移
                if(dp[i][0]==dp[i-1][0])  plan[i][0]=plan[i-1][0];  //记录方案数
                else plan[i][0]=i-1;

                if(i>=k)
                {
                    dp[i][1]=max(dp[i-1][1],dp[i-k][0]+sum[i-1]);
                    if(dp[i][1]==dp[i-1][1])  plan[i][1]=plan[i-1][1];
                    else plan[i][1]=i-1;

                    dp[i][2]=max(dp[i-1][2],dp[i-k][1]+sum[i-1]);
                    if(dp[i][2]==dp[i-1][2])  plan[i][2]=plan[i-1][2];
                    else plan[i][2]=i-1;
                }
            }
        }
        vector<int> res;
        int st2=plan[N-k+1][2]; //求方案
        int st1=plan[st2-k+1][1];
        int st0=plan[st1-k+1][0];
        res.push_back(st0);
        res.push_back(st1);
        res.push_back(st2);
        return res;
    }
```



