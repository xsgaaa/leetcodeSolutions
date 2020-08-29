### leetcode [887. 鸡蛋掉落](https://leetcode-cn.com/problems/super-egg-drop/)

```cpp
/*
	解法：动态规划。
	参考：https://zxi.mytechroad.com/blog/?s=887
*/
```

```cpp
vector<vector<int>> dp;
    int superEggDrop(int K, int N) {
        dp=vector<vector<int>>(K+1,vector<int>(N+1,-1));
        return dfs(K,N);
    }
private:
    int dfs(int K,int N)
    {
        if(K==0 || N==0)    return dp[K][N]=0;
        if(K==1)    return dp[1][N]=N;
        if(N==1)    return dp[K][1]=1;
        if(dp[K][N]!=-1)    return dp[K][N];
        int l=1,r=N+1;
        while(l<r)
        {
            int m=(l+r)/2;
            int ret1=dfs(K-1,m-1);
            int ret2=dfs(K,N-m);
            if(ret1>=ret2)
                r=m;
            else
                l=m+1;
        }
        dp[K][N]=1+dfs(K-1,l-1);   //这里要用dfs，否则最后l的地方可能没有计算过，导致出错。
        return dp[K][N];
    }
```

