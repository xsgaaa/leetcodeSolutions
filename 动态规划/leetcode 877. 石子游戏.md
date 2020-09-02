### leetcode [877. 石子游戏](https://leetcode-cn.com/problems/stone-game/)

```cpp
/*
	解法;动态规划。博弈型DP。
	与Leetcode 486预测赢家 一个套路
*/
```

```cpp
bool stoneGame(vector<int>& piles) {
        int N=piles.size();
        int dp[N][N];
        memset(dp,0,sizeof dp);
        for(int i=0;i<N;i++)    dp[i][i]=piles[i];
        for(int i=N-2;i>=0;i--)
        {
            for(int j=i+1;j<N;j++)
                dp[i][j]=max(piles[i]-dp[i+1][j],piles[j]-dp[i][j-1]);
        }
        return dp[0][N-1]>0;
    }
```

