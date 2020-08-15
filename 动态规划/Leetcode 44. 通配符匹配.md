### Leetcode 44. 通配符匹配

解法：动态规划

```cpp
与leetcode 10.正则表 达式具有及其类似的做法。
```

```cpp
bool isMatch(string s, string p) {
    int N=s.size(),M=p.size();
    bool dp[N+1][M+1];
    memset(dp,false,sizeof dp);
    dp[0][0]=true;
    for(int j=0;j<M;j++)
    {
        if(p[j]=='*')
        {
            for(int i=0;i<=N;i++)
            {
                if(j==0)
                    dp[i][j+1]=true;
                else
                    dp[i][j+1]=dp[i][j];
            }
        }
    }
    for(int i=1;i<=N;i++)
    {
        for(int j=1;j<=M;j++)
        {
            if((s[i-1]==p[j-1] || p[j-1]=='?') && dp[i-1][j-1])
                dp[i][j]=true;
            else if(p[j-1]=='*')
                dp[i][j]=dp[i-1][j] || dp[i-1][j-1] || dp[i][j-1];
        }
    }
    return dp[N][M];
}
```

