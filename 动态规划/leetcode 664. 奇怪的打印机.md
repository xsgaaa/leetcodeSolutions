### leetcode [664. 奇怪的打印机](https://leetcode-cn.com/problems/strange-printer/)

```cpp
/*
	解法：区间dp。
	见注释。
*/
```



```cpp
int dp[100][100];
int strangePrinter(string s) {
    memset(dp,0,sizeof dp);	//记忆化递归时，一般初始化为0或者-1
    return dfs(s,0,s.size()-1);
}
private:
int dfs(string &s,int l,int r)
{
    if(l>r) return 0;	//边界条件
    if(dp[l][r]>0)  return dp[l][r];	//当值大于0或者不为-1，表示之前计算过，返回结果
    //这里要先计算一下，否则下面取最小值的时候会一直取到0，得不到正确的结果
    //而且当l==r时，这个将会触发l>r那个边界条件，所以这步必不可少。
    dp[l][r]=dfs(s,l,r-1)+1;		
    //接下来是枚举区间[l,r)
    for(int i=l;i<r;i++)
    {
        if(s[i]==s[r])
        {//如果s[i]==s[r]，那么[l,i]以及s[r]将会一起打印,[i+1,r-1]将会与之分开打印
            dp[l][r]=min(dp[l][r],dfs(s,l,i)+dfs(s,i+1,r-1));
        }
    }
    return dp[l][r];
}
```

