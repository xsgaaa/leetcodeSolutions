### leetcode [77. 组合](https://leetcode-cn.com/problems/combinations/)

```cpp
/*
	解法：DFS
*/
```

```cpp
vector<vector<int>> res;
    vector<int> tmpres;
    void dfs(int st,int cnt,int n,int k)
    {
        if(cnt==k)
        {
            res.push_back(tmpres);
            return;
        }
        if(st>n)    return ;
        for(int i=st;i<=n;i++)
        {
            tmpres.push_back(i);
            dfs(i+1,cnt+1,n,k);
            tmpres.pop_back();
        }
    }
    vector<vector<int>> combine(int n, int k) {
        k=min(k,n);
        dfs(1,0,n,k);
        return res;
    }
};
```

