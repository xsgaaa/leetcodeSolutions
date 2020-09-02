### leetcode [685. 冗余连接 II](https://leetcode-cn.com/problems/redundant-connection-ii/)

```cpp
/*
	解法：并查集。
	参考684 题，如果存在冗余连接，那么一定有环。
	此外，这题为无向图，存在一种特殊的情况，就是某个结点可能有两个父节点。而且其中一个父节点在环中。
*/
```



```cpp
vector<int> findRedundantDirectedConnection(vector<vector<int>>& edges) {
        int N=edges.size();
        int parent[N+1];	//存储每个结点的父节点
        int fa[N+1];		//并查集
        memset(parent,0,sizeof parent);
        memset(fa,0,sizeof fa);
        for(int i=1;i<=N;i++)
        {
            fa[i]=i;					//初始化并查集
        }
        vector<int> ans1,ans2;			//存储结果
        for(auto & e:edges)
        {
            int u=e[0],v=e[1];
            if(parent[v])				//如果结点v已经有父节点了，这时有两个parent了
            {
                ans1={parent[v],v};		//将两个parent进行保存
                ans2=e;
                e[0]=e[1]=-1;			//删除这条边
                break;
            }
            parent[v]=u;
        }
        for(auto &e:edges)
        {
            int u=e[0],v=e[1];
            if(u<0 || v<0)  continue;	//碰到-1那条边

            int pu=find(u,fa);
            int pv=find(v,fa);
            if(pv==pu)			//删除了一条parent边，此时又碰到了，代表这条边是构成环的一部分，应该删去这条边
            {
                return ans1.empty()?e:ans1;	//如果ans1为空，代表没有两个parents。否则删除ans1
            }
            else if(pv<pu)
            {
                fa[pu]=pv;	//进行合并，大值优先向小值合并
            }
            else 
            {
                fa[pv]=pu;
            }
        }
    	//正常情况下，必定有环。
    	//如果没有环，那么很可能是删除的那个结点是构成环的一部分，将删除的边返回即可。
        return ans2;		
    }
    int find(int i,int fa[])
    {
        if(fa[i]!=i)
            fa[i]=find(fa[i],fa);
        return fa[i];
    }
```

