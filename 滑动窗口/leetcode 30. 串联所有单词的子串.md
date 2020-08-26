### leetcode [30. 串联所有单词的子串](https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words/)

```cpp
/*
解法：滑动窗口+哈希。
参考：https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words/solution/30-by-ikaruga/
*/
```



```cpp
vector<int> findSubstring(string s, vector<string>& words) {
        if(s.empty()|| words.empty())   return {};
        int n=s.size(),m=words.size(),len=words[0].size();
        unordered_map<string,int> mp;
        for(auto & w:words) mp[w]++;    //统计词频
        vector<int> ans;
        for(int i=0;i<len;i++)
        {//以[0,len-1]为起点，可以涵盖所有的可能
            int l=i,r=i;        //定义窗口的最左边
            int cnt=0;          //窗口内单词的个数
            unordered_map<string,int> tmp;  //临时的哈希表
            while(l+m*len<=n)
            {
                string str="";
                while(cnt<m)        //当窗口内单词的数量未达到要求时，扩展窗口
                {
                    str=s.substr(r,len);    //截取字符串
                    //如果不包含字符串或者字符串数量超出，则退出
                    if(mp.count(str)==0 || tmp[str]>=mp[str]) break;    
                    cnt++;      //窗口内单词的书数量增加
                    r+=len;     //窗口扩展
                    tmp[str]++;
                }
                //两个哈希相同，第一次知道还可以直接比较两个unordered_map是否相同
                if(tmp==mp) ans.push_back(l);
                if(tmp.count(str))
                {//包含str，左边界右移
                    tmp[s.substr(l,len)]--;
                    cnt--;
                    l+=len;
                }
                else
                {//不包含str，直接跳到右边界来，因为不可能满足要求了。
                    cnt=0;
                    r+=len;
                    l=r;
                    tmp.clear();
                }
            }
        }
        return ans;
    }
```

