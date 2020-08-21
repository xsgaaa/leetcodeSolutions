### leetcode [126. 单词接龙 II](https://leetcode-cn.com/problems/word-ladder-ii/)

解法：求最短路方案。需要用`BFS`来建图，`DFS`来求方案。

注意：由于到`endWord`的最短路径可能有多条，因此不能随便剪枝。如下图。需要将同一层的其余路径都进行保存。

因此需要记录单词第一次出现所在的层数。

此外，为了防止`DFS`搜索过程中搜索到其他支路上浪费时间。这里构造逆邻接矩阵。直接从结果向起点进行搜索，构造结果。

图来源：https://zxi.mytechroad.com/blog/searching/leetcode-126-word-ladder-ii/

![img](http://zxi.mytechroad.com/blog/wp-content/uploads/2017/09/126-ep72-3.png)

```cpp
vector<string> v;
    vector<vector<string>> ans;
    void dfs(string end,string & st,unordered_map<string,vector<string>> & mp)
    {
        if(end==st)
        {
            ans.push_back(v);
            reverse(ans.back().begin(),ans.back().end());
            return;
        }
        for(auto & str:mp[end])
        {
            v.push_back(str);
            dfs(str,st,mp);
            v.pop_back();
        }
    }
    vector<vector<string>> findLadders(string beginWord, string endWord, vector<string>& wordList) {
        unordered_set<string> dict(wordList.begin(),wordList.end());
        if(!dict.count(endWord))    return {};
        if(dict.count(beginWord))   dict.erase(beginWord);
        unordered_map<string,vector<string>> mp;
        unordered_map<string,int> depth{{beginWord,1}};
        queue<string> q;
        q.push(beginWord);
        while(!q.empty())
        {
            string str=q.front();q.pop();
            string s(str);
            for(int i=0;i<str.size();i++)
            {
                for(char c='a';c<='z';c++)
                {
                    s[i]=c;
                    if(!dict.count(s))  continue;
                    if(!depth.count(s))
                    {
                        depth[s]=depth[str]+1;
                        q.push(s);
                        mp[s].push_back(str);
                    }
                    else if(depth[s]==depth[str]+1)
                    {
                        mp[s].push_back(str);
                    }
                }
                s[i]=str[i];
            }
        }
        v.push_back(endWord);
        dfs(endWord,beginWord,mp);
        return ans;
    }
```

