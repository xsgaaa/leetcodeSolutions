### leetcode [329. 矩阵中的最长递增路径](https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix/)

```cpp
/*
	解法:DFS+记忆化递归。
*/
```



```cpp
int dirs[4][2]={{1,0},{-1,0},{0,1},{0,-1}};
    int res=0;
    int longestIncreasingPath(vector<vector<int>>& matrix) {
        if(matrix.empty() || matrix[0].empty()) return 0;
        N=matrix.size(),M=matrix[0].size();
        dp=vector<vector<int>>(N,vector<int>(M,0));
        for(int i=0;i<N;i++)
        {
            for(int j=0;j<M;j++)
            {
                res=max(res,dfs(matrix,i,j));
            }
        }
        return res;
    }
    int dfs(vector<vector<int>>& matrix,int i,int j)
    {
        if(dp[i][j]>0)  return dp[i][j];
        int ans=0;
        for(int k=0;k<4;k++)
        {
            int ni=i+dirs[k][0],nj=j+dirs[k][1];
            if(ni<0 || nj<0 || ni>=N  || nj>=M || matrix[ni][nj]<=matrix[i][j])  continue;
            ans=max(ans,dfs(matrix,ni,nj));
        }
        return dp[i][j]=ans+1;
    }
    private:
        int N;
        int M;
        vector<vector<int>> dp;
```

