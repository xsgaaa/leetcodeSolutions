### leetcode [87. 扰乱字符串](https://leetcode-cn.com/problems/scramble-string/)

```cpp
/*
	解法：记忆化递归。
	如果不记忆化，单纯地递归，必然会超时。
*/
```

```cpp
vector<vector<vector<int>>> dp;
    bool dfs(string &s1,string &s2,int l1,int h1,int l2,int h2)
    {
        if(l1==h1)  return s1[l1]==s2[l2];
        if(dp[l1][h1][l2]!=-1)   return dp[l1][h1][l2];
        bool flag=false;
        for(int i=l1;i<h1;i++)
        {
           flag= flag || (dfs(s1,s2,l1,i,l2,l2+i-l1) &&  dfs(s1,s2,i+1,h1,l2+i-l1+1,h2));
           flag= flag || (dfs(s1,s2,l1,i,h2-(i-l1),h2) &&  dfs(s1,s2,i+1,h1,l2,h2-(i-l1)-1));
           if(flag)
           {
                dp[l1][h1][l2]=flag;
                return flag;
           }
        }
        dp[l1][h1][l2]=flag;
        return flag;
    }
    bool isScramble(string s1, string s2) {
        if(s1.size()!=s2.size())    return false;
        int n=s1.size();
        dp=vector<vector<vector<int>>>(n,vector<vector<int>>(n,vector<int>(n,-1)));
        return dfs(s1,s2,0,s1.size()-1,0,s2.size()-1);
    }
```

