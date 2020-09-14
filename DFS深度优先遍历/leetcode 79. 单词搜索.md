### leetcode [79. 单词搜索](https://leetcode-cn.com/problems/word-search/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       

```cpp
/*
	解法：四联通 区域的深度优先搜索
*/
```

```cpp
class Solution {
public:
    int N,M;
    int dirs[5]={1,0,-1,0,1};
    bool dfs(vector<vector<bool>> & vis,int i,int j,int cnt,string & word,vector<vector<char>> & board)
    {
        if(cnt==word.size())
        {
            return true;
        }
        for(int k=0;k<4;k++)
        {
            int ni=i+dirs[k],nj=j+dirs[k+1];
            if(ni<0 || ni>=N || nj<0 || nj>=M ||board[ni][nj]!=word[cnt] || vis[ni][nj])
                continue;
            vis[ni][nj]=true;
            if(dfs(vis,ni,nj,cnt+1,word,board)) return true;
            vis[ni][nj]=false;
        }
        return false;
    }
    bool exist(vector<vector<char>>& board, string word) {
        if(board.empty( )|| board[0].empty())   return false;
        if(word.empty()) return false;
        N=board.size(),M=board[0].size();
        vector<vector<bool>> vis(N,vector<bool>(M,0));	//必须要设置访问数组，否则会超时
        for(int i=0;i<N;i++)
        {
            for(int j=0;j<M;j++)
            {
                if(board[i][j]==word[0])
                {
                    vis[i][j]=true;
                    if(dfs(vis,i,j,1,word,board))
                        return true;
                    vis[i][j]=false;
                }
            }
        }
        return false;
    }
};
```

