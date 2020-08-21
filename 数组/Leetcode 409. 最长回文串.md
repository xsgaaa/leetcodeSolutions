### [Leetcode 409. 最长回文串](https://leetcode-cn.com/problems/longest-palindrome/)

```cpp
解法：利用unordered_map统计词频。如果字符出现偶数次，直接相加。出现奇数次，则加上奇数次-1。并设置标志代表出现过奇数次。

最后如果出现过奇数次，再加上1。
```

```cpp
int longestPalindrome(string s) {
        int N=s.size();
        unordered_map<char,int> mp;
        for(auto &c:s)
        {//统计词频
            mp[c]++;
        }
        int cnt=0;
        bool flag=false;
        for(auto & p:mp)
        {
            if(p.second%2==0)//偶数的话全部加入
                cnt+=p.second;
            else
            {
                cnt+=p.second-1;//奇数的话，减去一个，添加偶数个
                flag=true;      //并且设置标志
            }
        }
        if(flag)    return cnt+1;   //中间可以再补一个奇数的字符
        return cnt;         //没有奇数，直接返回
    }
```





