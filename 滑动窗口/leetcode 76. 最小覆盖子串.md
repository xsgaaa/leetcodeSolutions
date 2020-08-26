### leetcode [76. 最小覆盖子串](https://leetcode-cn.com/problems/minimum-window-substring/)



```cpp
/*
	解法：滑动窗口。
	本题的关键是在于
*/
```



```cpp
string minWindow(string s, string t) {
        if(s.empty() || t.empty())  return "";
        int n=s.size(),m=t.size();
        unordered_map<char,int> mp;
        for(auto &c:t)  mp[c]++;
        int l=0,r=0;
        unordered_map<char,int> tmp;
        int cnt=0;
        int left,len=INT_MAX;
        while(r<n)
        {   
            if(mp.count(s[r]) && tmp[s[r]]<mp[s[r]])
                cnt++;
            tmp[s[r]]++;
            while(cnt>=m)
            {
                if(r-l+1<len)
                {
                    left=l;
                    len=r-l+1;
                }
                if(mp.count(s[l]) &&tmp[s[l]]<=mp[s[l]])
                    cnt--;
                tmp[s[l]]--;
                l++;
            }
            r++;
        }
        return len==INT_MAX?"":s.substr(left,len);
    }
```

