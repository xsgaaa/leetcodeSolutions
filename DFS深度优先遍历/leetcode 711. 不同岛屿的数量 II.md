### leetcode [711. 不同岛屿的数量 II](https://leetcode-cn.com/problems/number-of-distinct-islands-ii/)

```cpp
/*
	解法:深度优先搜索。
	重复的情况很多，注意去重。
	真是让我见识到了set的威力，去重大神器啊。
*/
```



```cpp
typedef pair<int,int> PII;
    #define x first
    #define y second
    int numDistinctIslands2(vector<vector<int>>& grid) {
        if(grid.empty() || grid[0].empty())  return 0;
        int N=grid.size(),M=grid[0].size();
        set<vector<PII>> S;
        for(int i=0;i<N;i++)
        {
            for(int j=0;j<M;j++)
            {
                if(grid[i][j])
                {
                    vector<PII> shape;
                    helper(grid,i,j,shape);
                    S.insert(normalize(shape));
                }
            }
        }
        return S.size();
    }
    private:
        void helper(vector<vector<int>>& grid,int i,int j,vector<PII> & shape)
        {
            if(i<0 || i>=grid.size() || j<0 || j>=grid[0].size() || grid[i][j]==0)   return;
            shape.push_back({i,j});
            grid[i][j]=0;
            helper(grid,i+1,j,shape);
            helper(grid,i-1,j,shape);
            helper(grid,i,j+1,shape);
            helper(grid,i,j-1,shape);
        }
        vector<PII> normalize(vector<PII> & shape)
        {
            vector<vector<PII>> shapes(8);
            for(auto & a:shape)
            {
                int i=a.x,j=a.y;
                shapes[0].push_back({i,j});
                shapes[1].push_back({i,-j});
                shapes[2].push_back({-i,j});
                shapes[3].push_back({-i,-j});
                shapes[4].push_back({j,-i});
                shapes[5].push_back({j,i});
                shapes[6].push_back({-j,-i});
                shapes[7].push_back({-j,i});
            }
            for(auto & a:shapes)
            {
                //在a内部进行排序，然后相减得到相对值
                sort(a.begin(),a.end());
                for(int i=a.size()-1;i>=0;i--)
                {
                    a[i].x -= a[0].x;
                    a[i].y -= a[0].y;
                }
            }
            //对8组数据进行排序，得到最小值作为特征值
            sort(shapes.begin(),shapes.end());
            return shapes[0];
        }
```

