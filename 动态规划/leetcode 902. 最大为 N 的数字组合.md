### leetcode [902. 最大为 N 的数字组合](https://leetcode-cn.com/problems/numbers-at-most-n-given-digit-set/)

```cpp
/*
	解法：数位dp,记忆化递归。
*/
```

```cpp
vector<int> dp;
    int atMostNGivenDigitSet(vector<string>& D, int N) {
        string str=to_string(N);    //转换成字符串
        vector<int> vec;            //将D中的字符串转换成数字
        for(auto &c:D)
            vec.push_back(stoi(c));
        sort(vec.begin(),vec.end());//排序
        dp=vector<int>(str.size()+1,-1);    //构造记忆化数组
        return dfs(vec,str,0,0,false,true);
    }
private:
    int dfs(vector<int> & vec,string & str,int cnt,int num,bool lead,bool limit)
    {//vec中为待选的数字，str为字符串,cnt为遍历到第几位了，num表示目前有几位非0
    //lead表示是否有前导0，limit表示是否和原字符串接近了，也就是前几位是否都与原串相同了
        if(cnt==str.size() && num)  return 1;   //递归终止
        if(cnt==str.size() && !num)  return 0;
        //没有前导0,而且没有接近原串
        if(!limit && !lead && dp[str.size()-cnt]!=-1)   return dp[str.size()-cnt];

        int ret=0;
        int maxv=limit?str[cnt]-'0':9;  //目前位能取到的最大数字
        for(auto &i:vec)
        {
            if(i<=maxv) //遍历，添加数字即可。如果limit已经为true，并且i==maxv，则limit才能继续保持true
                    ret+=dfs(vec,str,cnt+1,num+1,false,limit && i==maxv);
        }
        if(num==0)//只有之前全都为0,这里才能取前导0.
            ret+=dfs(vec,str,cnt+1,num,true,limit && 0==maxv);
        if(!limit && !lead)  dp[str.size()-cnt]=ret;
        return ret;
    }
```

