### leetcode [546. 移除盒子](https://leetcode-cn.com/problems/remove-boxes/)

```cpp
/*
	解法：动态规划，记忆化递归。
	见注释。
*/
```

```cpp
	int dp[100][100][100];
    //一般'移除'字眼必用区间dp
    //这题必须用三维dp,二维dp无法存储连续区间内有几个相同的元素，而且数据范围100以内，可以用三维dp
    int removeBoxes(vector<int>& boxes) {
        int N=boxes.size();
        memset(dp,-1,sizeof dp);
        return dfs(boxes,0,N-1,0);
    }
    int dfs(vector<int>& b,int l,int r,int k)
    {
        if(l>r) return 0;
        if(dp[l][r][k]!=-1) return dp[l][r][k];	//返回记忆化的结果
        while(l<r && b[r-1]==b[r])
        {//将一连串相同的数据进行统计(优化1)
        //当循环终止时,b[r-1]!=b[r],b[r]和原来的b[r]相同
            r--,k++;
        }
        //将r-1后面的K+1个元素先进行合并
        dp[l][r][k]=dfs(b,l,r-1,0)+(k+1)*(k+1);
        for(int i=l;i<r;i++) 
        {
            if(b[i]==b[r])//将i后面的k+1个元素附加到i之后 并 单独合并[i+1,r-1]的内容
                dp[l][r][k]=max(dp[l][r][k],dfs(b,l,i,k+1)+dfs(b,i+1,r-1,0));
        }
        return dp[l][r][k];
    }
```

