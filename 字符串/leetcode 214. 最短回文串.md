### leetcode [214. 最短回文串](https://leetcode-cn.com/problems/shortest-palindrome/)

```cpp
/*
	解法：利用KMP中的next数组来计算。
	此题实际上求原串中从起始位置开始的最长回文串，然后将剩余部分翻转到头部就行，
	直接求较难求。考虑将原数组翻转得到一个新串，加到原串的后面。然后求这整个串的next数组。
	由于数组中的元素可能有重复，在分界线处加一个‘#'号。
*/
```

```cpp
string shortestPalindrome(string s) {
        int sn=s.size();
        if(sn<=1)    return s;
        string str(s);
        reverse(str.begin(),str.end());
        s=' '+s+'#'+str;	//让有效字符串的下标从1开始
        int n=s.size()-1;
        int ne[n+1];
        memset(ne,0,sizeof ne);
    	//下面这段代码求从1开始的模式串的next数组。要背下来。
        for(int i=2,j=0;i<=n;i++)
        {
            while(j && s[i]!=s[j+1]) j=ne[j];
            if(s[i]==s[j+1])  j++;
            ne[i]=j;
        }
        return s.substr(sn+2,sn-ne[n])+s.substr(1,sn);
    }
```

