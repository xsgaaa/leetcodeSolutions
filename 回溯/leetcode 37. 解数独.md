### leetcode [37. 解数独](https://leetcode-cn.com/problems/sudoku-solver/)

```cpp
/*
	解法：DFS+回溯。
*/
```



```cpp
typedef pair<int,int> PII;
bool flag=false;
void dfs(int cnt,int n,vector<PII> &v,bitset<9> rows[],bitset<9> cols[],bitset<9> mat[],vector<vector<char>> & board)
{
    if(cnt==n)
    {
        flag=true;
        return;
    }
    int x=v[cnt].first,y=v[cnt].second;
    for(int i=1;i<=9;i++)
    {
        if(rows[x][i]==1 || cols[y][i]==1 || mat[x/3*3+y/3][i]==1) continue;
        rows[x][i]=1;
        cols[y][i]=1;
        mat[x/3*3+y/3][i]=1;
        board[x][y]=i+'0';

        dfs(cnt+1,n,v,rows,cols,mat,board);
        if(flag)    return;


        rows[x][i]=0;
        cols[y][i]=0;
        mat[x/3*3+y/3][i]=0;
        //board[x][y]='.';
    }
}
void solveSudoku(vector<vector<char>>& board) {
    vector<PII> v;
    bitset<9> rows[9],cols[9],mat[9];
    for(int i=0;i<9;i++)
    {
        for(int j=0;j<9;j++)
        {
            if(!isdigit(board[i][j]))   v.push_back({i,j});

            int num=board[i][j]-'0';

            rows[i][num]=1;
            cols[j][num]=1;
            mat[i/3*3+j/3][num]=1;
        }
    }

    dfs(0,v.size(),v,rows,cols,mat,board);
}
```

