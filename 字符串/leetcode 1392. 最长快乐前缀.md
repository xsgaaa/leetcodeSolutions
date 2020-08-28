### leetcode [1392. 最长快乐前缀](https://leetcode-cn.com/problems/longest-happy-prefix/)

```cpp
/*
	解法:其实就是求KMP算法中的next数组。
	套模板就行。
*/
```

```cpp
string longestPrefix(string s) {
        s.insert(s.begin(),' ');
        int n=s.size();
        int ne[n];
        memset(ne,0,sizeof ne);
        for(int i=2,j=0;i<n;i++)
        {
            while(j && s[i]!=s[j+1])   j=ne[j];
            if(s[i]==s[j+1])    j++;
            ne[i]=j;
        }
        return ne[n-1]==0?"":s.substr(1,ne[n-1]);
    }
```

