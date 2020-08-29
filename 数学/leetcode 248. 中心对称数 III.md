### leetcode [248. 中心对称数 III](https://leetcode-cn.com/problems/strobogrammatic-number-iii/)

```cpp
/*
	解法：DFS
	注意边界的判断。
*/
```



```cpp
int strobogrammaticInRange(string low, string high) {   
        int ret=0;
        dfs(low,high,"",ret);
        dfs(low,high,"0",ret);
        dfs(low,high,"1",ret);
        dfs(low,high,"8",ret);
        return ret;
    }
    void dfs(string & low,string &high,string str,int & ret)
    {
        if(str.size()>=low.size() && str.size()<=high.size())
        {
            if(str.size()==high.size() && str>high) return; //比high大，退出
            if((str.size()==low.size() && str>=low) || str.size()>low.size())
            {//大于等于low
                //str.size()==1的话，首部可以为0，否则，首部不能为0。数量增加。
                if(str.size()==1 || str[0]!='0') ret++;
            }        
        }
        if(str.size()+2<=high.size())
        {
            dfs(low,high,"0"+str+"0",ret);
            dfs(low,high,"1"+str+"1",ret);
            dfs(low,high,"6"+str+"9",ret);
            dfs(low,high,"8"+str+"8",ret);
            dfs(low,high,"9"+str+"6",ret);
        }
    }
```

