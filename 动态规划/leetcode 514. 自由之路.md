### leetcode [514. 自由之路](https://leetcode-cn.com/problems/freedom-trail/)

```cpp
/*
	解法：动态规划。
	这个很像旅行商问题的解法。
*/
```



```cpp
int findRotateSteps(string ring, string key) {
        unordered_map<char,vector<int>> mp;		//记录string中每个字符出现的位置
        int N=ring.size(),M=key.size();
        for(int i=0;i<N;i++)    mp[ring[i]].push_back(i);
        int dp[M][N];
    	//dp[i][j]表示到达key中第i个字符，其在ring中的第j个位置所需的最小步数
        memset(dp,0x3f,sizeof dp);		//求最小值，初始化最大值
        for(auto &pos:mp[key[0]])
        {
            dp[0][pos]=min(pos,N-pos);	//首位 需要特殊处理。
        }
        for(int k=1;k<M;k++)
        {
            for(auto &i:mp[key[k]])		//枚举第k个字符所在的位置
            {
                for(auto &j:mp[key[k-1]])		//枚举第k-1个字符所在的位置
                {
                    //进行状态转移
                    dp[k][i]=min(dp[k][i],dp[k-1][j]+min(abs(i-j),N-abs(i-j)));
                }
            }
        }
        int res=INT_MAX;
        for(auto &i:mp[key[M-1]])
        {//枚举key[M-1]所在的位置，得出最终结果
            res=min(res,dp[M-1][i]);
        }
        return res+M;	//由于每一步都要确认，需要加上一个key的长度
    }
```

