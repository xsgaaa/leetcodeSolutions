### leetcode [233. 数字 1 的个数](https://leetcode-cn.com/problems/number-of-digit-one/)

```cpp
/*
	解法：数位dp。记忆化递归。
	详情见代码注释。
*/
```

```cpp
int a[14];
    int dp[14][14];    //定义状态:pos表示当前在n的哪个位置上
    //state表示当前有多少个1
    int dfs(int pos,int state,int limit)
    {
        if(!pos)    return state;       //当pos到达末尾时，返回结果
        //记录limit==0时的结果，此时将结果返回
        //limit==0表示前有位数并没有达到最大值
        if(!limit && dp[pos][state]!=-1)    return dp[pos][state];
        //如果前面都达到了最大值，比如n=12345，前面已经是123__了，那么接下来最大值只能取4了
        int res=0,up=limit?a[pos]:9;
        for(int i=0;i<=up;i++)
        {//尝试取每一位的数字。如果i==1，state将会增加。
            //只有当前面都为state,而且当前又取到最大值时，limit才能为1
            res+=dfs(pos-1,state+(i==1),limit && i==a[pos]);
        }
        //当limit==0时，记录结果。limit=1时的结果将不会被记录。
        return limit?res:dp[pos][state]=res;
    }
    int countDigitOne(int n) {
        memset(dp,-1,sizeof dp);    //初始化所有数组为-1,
        int len=0;
        while(n)
        {//记录n的各位数字，从1-len.
            a[++len]=n%10;
            n /=10;
        }
        return dfs(len,0,1);//limit位默认为true
    }
```

