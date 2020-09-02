### leetcode [684. 冗余连接](https://leetcode-cn.com/problems/redundant-connection/)

```cpp
/*
	解法：并查集模板题。
*/
```

```cpp
int fa[1001];
    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        int N=edges.size();
        for(int i=1;i<=N;i++)
            fa[i]=i;
        for(auto & e:edges)
        {
            int f0=find(e[0]);	//找e[0]的父节点
            int f1=find(e[1]);	//找e[1]的父节点
            if(f0<f1)
            {
                fa[f1]=f0;		
            }
            else if(f0>f1)
            {
                fa[f0]=f1;
            }
            else{
                return e;
            }
        }
        return {};
    }
    int find(int i)
    {
        if(fa[i]!=i)
            fa[i]=find(fa[i]);
        return fa[i];
    }
```

