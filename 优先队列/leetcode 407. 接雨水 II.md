### leetcode 407. 接雨水 II

解法：优先队列。

```cpp
//利用木桶原理，一个桶里能装的水量由桶周围最低的板子所决定
//所以利用优先队列，优先弹出最小高度的值
//从最小的值开始向周围更矮的地方灌水
//等于从木桶周围最低的板子向桶里灌水，灌满水后，高度趋向一致
```



```cpp
typedef struct Cell{
        int x,y,h;
        Cell(int _x,int _y,int _h):x(_x),y(_y),h(_h){};
        bool operator < (const Cell & c) const
        {//重载小于号，默认生成大根堆,降序排列。通过改变符号，变成小根堆升序排列
            return h>c.h;
        }
    }Cell;
    int dirs[4][2]={{1,0},{-1,0},{0,1},{0,-1}}; //定义方向矢量
    int trapRainWater(vector<vector<int>>& heightMap) {
        int N=heightMap.size(),M=heightMap[0].size();
        priority_queue<Cell> pq;    //定义优先队列
        bool vis[N][M];
        memset(vis,0,sizeof vis);
        for(int i=0;i<N;i++)
        {
            for(int j=0;j<M;j++)
            {
                if(i==0 || j==0 || i==N-1 || j==M-1)
                {//将最外围的数据插入优先队列中
                    pq.push(Cell(i,j,heightMap[i][j]));
                    vis[i][j]=true;
                }
            }
        }
        //利用木桶原理，一个桶里能装的水量由桶周围最低的板子所决定
        //所以利用优先队列，优先弹出最小高度的值
        int res=0;
        while(!pq.empty())
        {
            auto t=pq.top();pq.pop();
            for(int i=0;i<4;i++)
            {//遍历四个反向
                int x=t.x+dirs[i][0],y=t.y+dirs[i][1];
                if(x<0 || x>=N || y<0 || y>=M || vis[x][y])
                    continue;       //检查是否满足边界条件
                if(heightMap[x][y]<t.h)
                {//如果周围有比其还小的，加上差值
                    res+=t.h-heightMap[x][y];
                }
                vis[x][y]=true;     //置为已访问
                //等于从木桶周围最低的板子向桶里灌水，灌满水后，高度趋向一致
                pq.push({x,y,max(t.h,heightMap[x][y])});    
            }
        }
        return res;
    }
```



