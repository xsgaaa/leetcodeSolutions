### Leetcode 44. 通配符匹配



```cpp
/*
	解法：动态规划
	与leetcode 10.正则表 达式具有及其类似的做法。
		dp[i][j] 表示 s串中[0...i]与p串中[0...j]是否匹配
		if(p[j-1]=='？' || p[j-1]==s[i-1])	
			dp[i][j]=dp[i-1][j-1];
		if(p[j-1]=='*')
			dp[i][j]=dp[i-1][j] || dp[i][j-1] || dp[i-1][j-1];
  */  
```

```cpp
bool isMatch(string s, string p) {
        int m=s.size(),n=p.size();
        bool dp[m+1][n+1];
        memset(dp,0,sizeof dp);
        dp[0][0]=true;
        for(int i=1;i<=n;i++)
        {
            if(p[i-1]=='*') dp[0][i]=true;
            else break;
        }
        for(int i=1;i<=m;i++)
        {
            for(int j=1;j<=n;j++)
            {
                if(p[j-1]=='?' || p[j-1]==s[i-1])
                {
                    dp[i][j]=dp[i-1][j-1];	//这一步没啥好说的，水到渠成
                }
                else if(p[j-1]=='*')	//这一步的if条件必须加，不然会出错。
                //如果不加if条件判断，那么p[j-1]!=s[i-1]的情况也会进入这个循环，导致错误
                {
                    //dp[i-1][j-1]表示p[j-1]==s[i-1]
                    //dp[i][j-1]表示p[j-1]=''
                    //dp[i-1][j]表示p[j-1]匹配了s[i-1]之前的字符串
                    dp[i][j]=dp[i-1][j] || dp[i][j-1] || dp[i-1][j-1];
                }
            }
        }
        return dp[m][n];
    }
```

