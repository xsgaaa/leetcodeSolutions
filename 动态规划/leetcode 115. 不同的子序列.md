### leetcode [115. 不同的子序列](https://leetcode-cn.com/problems/distinct-subsequences/)

```cpp
/*
	解法：动态规划。
	状态定义: dp[i][j] 表示s中以j结尾的字符串包含t中以i结尾的字符串的数目
	状态转移：
		if(s[j-1]==t[i-1]) dp[i][j]=dp[i][j-1]		//跳过s[j-1]
									+dp[i-1][j-1]	//匹配s[j-1]和t[i-1]
		else dp[i][j]=dp[i][j-1]	//跳过s[j-1]
	初始化：
		dp[0][i]=1;表示任意字符串都包含空串。
*/
```

```cpp
int numDistinct(string s, string t) {
        int ls=s.size();
        int lt=t.size();
        long dp[lt+1][ls+1];   //表示s中以j结尾的字符串包含t中以i结尾的字符串的数目
        memset(dp,0,sizeof dp);
        //当t为空串时，s必然包含t,所以个数为1
        fill(dp[0],dp[0]+ls+1,1);
        for(int i=1;i<=lt;i++)
        {
            for(int j=1;j<=ls;j++)
            {
                dp[i][j]=dp[i][j-1];    //表示跳过s[j]
                if(t[i-1]==s[j-1])
                {
                    dp[i][j]+=dp[i-1][j-1]; //表示匹配t[i-1]和s[j-1]
                }
            }
        }
        return dp[lt][ls];  //最终即为结果
    }
```

