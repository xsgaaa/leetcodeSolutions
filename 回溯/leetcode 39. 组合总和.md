### leetcode [39. 组合总和](https://leetcode-cn.com/problems/combination-sum/)

```cpp
/*
	解法：回溯。
*/
```

```cpp
vector<vector<int>> res;
    vector<int> tmpres;
    void dfs(int st,int tar,vector<int>&ca)
    {
        if(tar==0)
        {
            res.push_back(tmpres);
            return;
        }
        if(tar<0)   return;
        for(int i=st;i<ca.size();i++)
        {//注意这里要控制起点，下一次访问只能在当前位置及其之后
            tmpres.push_back(ca[i]);
            dfs(i,tar-ca[i],ca);
            tmpres.pop_back();
        }
    }
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        sort(candidates.begin(),candidates.end());
        dfs(0,target,candidates);
        return res;
    }
```

