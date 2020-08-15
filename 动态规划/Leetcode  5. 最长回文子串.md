### Leetcode  5. 最长回文子串

方法1:采用**中心扩散法**

注意边界条件。此外扩散的时候有两种不同的类别，分别对应着奇数个字符和偶数个字符

```cpp
string longestPalindrome(string s) {
        int N=s.size();
        if(N<2)    return s;	//边界条件需注意
        int cnt=0,st=0;
        for(int i=0;i<N;i++)
        {//中心扩散
            int l=i,r=i+1;		//对应偶数个字符
            while(l>=0 && r<N && s[l]==s[r])
                l--,r++;
            if(cnt<r-l-1)
            {
                cnt=r-l-1;
                st=l+1;
            }
            l=i-1,r=i+1;
            while(l>=0 && r<N && s[l]==s[r])
                l--,r++;		//对应奇数个字符,中间需要用一个字符
            if(cnt<r-l-1)
            {
                cnt=r-l-1;
                st=l+1;
            }    
        }
        return s.substr(st,cnt);
    }
```

