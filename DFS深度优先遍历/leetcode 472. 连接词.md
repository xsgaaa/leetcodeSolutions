### leetcode [472. 连接词](https://leetcode-cn.com/problems/concatenated-words/)

```cpp
/*
	解法：DFS。利用string_view类,并且如果知道字符串满足要求了，立马返回。
*/
```

```cpp
unordered_set<string_view> S;
bool dfs(const string_view & s,int st,int cnt)
{
    if(st==s.size() && cnt>=2)  return true;
    if(st==s.size())   return false;
    bool flag=false;
    for(int i=1;i<=s.size()-st;i++)
    {
        if(S.count(s.substr(st,i)))
        {
            flag=flag || dfs(s,st+i,cnt+1);
        }  
        if(flag)    return true;
    }
    return false;
}
vector<string> findAllConcatenatedWordsInADict(vector<string>& words) {
    for(auto & w:words)
        S.insert(w);
    vector<string> ans;
    for(auto & w:words)
    {
        if(w.size()==0) continue;
        if(dfs(w,0,0))
            ans.push_back(w);
    }
    return ans;
}
```

