### leetcode 221. 最大正方形

解法1：利用动态规划。

```cpp
dp[i][j]表示以(i,j)为右下角的正方形的边长.
    则dp[i][j]=min(dp[i-1][j-1],dp[i-1][j],dp[i][j-1]);
对于此状态转移的方程可以见下图。可见以dp[i][j]为右下角的正方形受其左上方、上方、左侧的正方形的大小的约束。
图来源：https://leetcode-cn.com/problems/maximal-square/solution/li-jie-san-zhe-qu-zui-xiao-1-by-lzhlyle/
```



![img](https://pic.leetcode-cn.com/8c4bf78cf6396c40291e40c25d34ef56bd524313c2aa863f3a20c1f004f32ab0-image.png)

```cpp
int maximalSquare(vector<vector<char>>& m) {
        if(m.empty() || m[0].empty())   return 0;
        int N=m.size(),M=m[0].size();
        int dp[N+1][M+1];
        memset(dp,0,sizeof dp);
        int len=0;
        for(int i=0;i<N;i++)
        {
            for(int j=0;j<M;j++)
            {
                if(m[i][j]=='1')
                {
                    dp[i+1][j+1]=min(dp[i][j],min(dp[i][j+1],dp[i+1][j]))+1;
                    len=max(len,dp[i+1][j+1]);
                }   
            }
        }
        return len*len;
    }
```

解法2：利用单调栈。(**时间稍微慢一些**)

```cpp
这题与 leetcode 85 题具有异曲同工之妙。只不过是85题中求的是最大的长方形的面积，这里求得是最大的正方形的面积。
需要在弹栈的是时候取长和宽的最小值作为正方形的边长即可。
这种方法可能容易想到一些。
```

```cpp
int maximalSquare(vector<vector<char>>& m) {
        if(m.empty()|| m[0].empty())    return 0;
        int N=m.size(),M=m[0].size();
        vector<int> dp(M+2,0);
        int res=0;
        for(int i=0;i<N;i++)
        {
            for(int j=0;j<M;j++)
            {
                dp[j+1]=m[i][j]=='0'?0:dp[j+1]+1;
            }
            res=max(res,maxArea(dp));
        }
        return res;
    }
    int maxArea(vector<int> h)
    {
        stack<int> st;
        int maxlen=0;
        for(int i=0;i<h.size();i++)
        {
            while(!st.empty() && h[st.top()]>h[i])
            {
                int hi=h[st.top()];st.pop();
                maxlen=max(maxlen,min(i-st.top()-1,hi));
            }
            st.push(i);
        }
        return maxlen*maxlen;
    }
```

