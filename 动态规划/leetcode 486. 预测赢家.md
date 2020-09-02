### leetcode [486. 预测赢家](https://leetcode-cn.com/problems/predict-the-winner/)

```cpp
/*
	解法：动态规划。博弈型DP。
	dp[i][j]表示以当前选手作为先手选择之后，比另外一个选手多的分数（净胜分）.
	则dp[i][j]有两种可能:
		(1) 当前选手如果选择nums[i]，则另一个选手在dp[i+1][j]中作为先手。dp[i][j]=nums[i]-dp[i+1][j]
		(2) 当前选手如果选择nums[j]，则另一个选手在dp[i][j-1]中作为先手。dp[i][j]=nums[j]-dp[i][j-1]
	最后 dp[i][j]取其中的最大值即可。
	
	初始条件下：dp[i][i]=nums[i]。表示只剩一堆的情况下,先手将获取所有的，后手没有选择机会了。先手比后手多的。
	
	注意循环的遍历顺序。见下图：
	dp[i][j](橙色部分)由其左边（红色）和下边(红色)转移过来。所以要先计算左边和下边。
	故第一层循环i要逆序(计算下边)，第一层循环j要正序(计算左边)。
*/
```



![leetcode486](picture\leetcode486.png)

```cpp
bool PredictTheWinner(vector<int>& nums) {
        int  N=nums.size();
        int dp[N][N];
        memset(dp,0,sizeof dp);
        for(int i=0;i<N;i++)    dp[i][i]=nums[i];
        for(int i=N-2;i>=0;i--)
        {
            for(int j=i+1;j<N;j++)
            {
                dp[i][j]=max(nums[i]-dp[i+1][j],nums[j]-dp[i][j-1]);
            }
        }
        return dp[0][N-1]>=0;
    }
```



```cpp
//由于i只与i+1有关，可以只用一维表示
bool PredictTheWinner(vector<int>& nums) {
        int  N=nums.size();
        int dp[N];
        memset(dp,0,sizeof dp);
        for(int i=0;i<N;i++)    dp[i]=nums[i];
        for(int i=N-2;i>=0;i--)
        {
            for(int j=i+1;j<N;j++)
            {
                dp[j]=max(nums[i]-dp[j],nums[j]-dp[j-1]);
            }
        }
        return dp[N-1]>=0;
    }
```

