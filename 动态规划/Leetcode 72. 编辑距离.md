### Leetcode 72. 编辑距离

解法：动态规划。

```cpp
定义dp[i][j]为以下标i结尾和以下标j结尾的最小的编辑距离。
状态转移为:
        w1[i]==w2[j]	dp[i][j]=dp[i-1][j-1]
        w1[i]!=w2[j]	dp[i][j]=min(dp[i-1][j],dp[i-1][j-1],dp[i][j-1])+1
边界条件：
        dp[i][0]=i,dp[0][j]=j;
```



```cpp
int minDistance(string w1, string w2) {
        int N=w1.size(),M=w2.size();
        int dp[N+1][M+1];
        memset(dp,0,sizeof dp);
        for(int i=1;i<=N;i++)    dp[i][0]=i;
        for(int j=1;j<=M;j++)    dp[0][j]=j;

        for(int i=1;i<=N;i++)
        {
            for(int j=1;j<=M;j++)
            {
                if(w1[i-1]==w2[j-1])
                    dp[i][j]=dp[i-1][j-1];
                else//删除,替换,插入
                    dp[i][j]=min(dp[i-1][j],min(dp[i-1][j-1],dp[i][j-1]))+1;
            }
        }
        return dp[N][M];
    }
```

