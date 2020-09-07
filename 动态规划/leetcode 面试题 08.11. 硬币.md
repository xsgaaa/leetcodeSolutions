### leetcode [面试题 08.11. 硬币](https://leetcode-cn.com/problems/coin-lcci/)

```cpp
/*
	解法:动态规划。
	是完全背包。
*/
```

```cpp
const int MOD=1000000007;
    int waysToChange(int n) {
        int dp[n+1];
        memset(dp,0,sizeof dp);
        dp[0]=1;
        vector<int> v={1,5,10,25};
        for(int i=0;i<4;i++)
        {
            for(int j=v[i];j<=n;j++)
            {
                dp[j]=(dp[j]+dp[j-v[i]])%MOD;
            }
        }
        return dp[n];
    }
```

