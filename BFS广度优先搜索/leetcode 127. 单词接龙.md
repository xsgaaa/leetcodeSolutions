### leetcode [127. 单词接龙](https://leetcode-cn.com/problems/word-ladder/)

解法：典型的最短路问题，采用`BFS`来做。

```cpp
int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        unordered_set<string> dict(wordList.begin(),wordList.end());
        if(!dict.count(endWord))    return 0;
        dict.erase(beginWord);
        unordered_map<string,int> depth{{beginWord,1}};
        queue<string> q;
        q.push(beginWord);
        while(!q.empty())
        {
            auto str=q.front();q.pop();
            string s(str);
            for(int i=0;i<str.size();i++)
            {
                for(char c='a';c<='z';c++)
                {
                    s[i]=c;
                    if(!dict.count(s))  continue;
                    if(s==endWord)  return depth[str]+1;
                    if(!depth.count(s))
                    {
                        q.push(s);
                        depth[s]=depth[str]+1;
                    }
                }
                s[i]=str[i];	//注意这一步
            }
        }
        return 0;
    }
```

