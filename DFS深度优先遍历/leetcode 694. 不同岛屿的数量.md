### leetcode [694. 不同岛屿的数量](https://leetcode-cn.com/problems/number-of-distinct-islands/)

```cpp
/*
	Leetcode 711题的简化版。
	解法:深度优先搜索，求相对坐标插入set中去重。
*/
```



```cpp
typedef pair<int,int> PII;
int numDistinctIslands(vector<vector<int>>& grid) {
    if(grid.empty() || grid[0].empty()) return 0;
    int m=grid.size(),n=grid[0].size();
    set<vector<PII>> S;
    for(int i=0;i<m;i++)
    {
        for(int j=0;j<n;j++)
        {
            if(grid[i][j])
            {
                vector<PII> shape;
                dfs(grid,i,j,shape);
                normalize(shape);
                S.insert(shape);
            }
        }
    }
    return S.size();
}
void dfs(vector<vector<int>>& grid,int x,int y,vector<PII> & shape)
{
    if(x<0 || x>=grid.size() || y<0 || y>=grid[0].size() || !grid[x][y])   return;
    shape.push_back({x,y});
    grid[x][y]=0;
    dfs(grid,x-1,y,shape);
    dfs(grid,x+1,y,shape); 
    dfs(grid,x,y-1,shape);
    dfs(grid,x,y+1,shape);
}
void normalize(vector<PII> &a)
{
    sort(a.begin(),a.end());
    for(int i=a.size()-1;i>=0;i--)
    {
        a[i].first -= a[0].first;
        a[i].second -= a[0].second;
    }
    return;
}
```

