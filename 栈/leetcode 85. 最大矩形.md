### leetcode 85. 最大矩形

解法：很难直接计算面积。二维矩阵中求矩形的面积采用的方法，是将二维矩阵压缩成一维的矩阵。统计每行中每个位置能取得的1的最大高度，就变成了84题。

```cpp
int maximalRectangle(vector<vector<char>>& m) {
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
private:
    int maxArea(vector<int> & h)
    {//利用leetcode第84题的结论，函数基本一样
        stack<int> st;
        int ret=0;
        for(int i=0;i<h.size();i++)
        {
            while(!st.empty() && h[st.top()]>h[i])
            {
                int cur=st.top();st.pop();
                ret=max(ret,(i-1-st.top())*h[cur]);
            }
            st.push(i);
        }
        return ret;
    }
```

