### leetcode [65. 有效数字](https://leetcode-cn.com/problems/valid-number/)

```cpp
/*
	解法：存储一个指针，进行全局扫描。
*/
```

```cpp
	int i=0;
    void scanspace(string &s)
    {
        while(s[i]==' ')    i++;
    }
    bool scanint(string &s)
    {
        if(s[i]=='+' || s[i]=='-')
            i++;
        return scanuint(s);
    }
    bool scanuint(string &s)
    {
        int tmp=i;
        while(s[i]!='\0' && isdigit(s[i]))
            i++;
        return i>tmp;
    }
    bool isNumber(string s) {
        if(s=="")   return false;
        scanspace(s);
        bool flag=scanint(s);
        if(s[i]=='.')
        {
            i++;
            flag=scanuint(s) || flag;	//小数点前面和后面只要有一处为true就行
        }
        if(s[i]=='e')
        {
            i++;
            flag=flag && scanint(s);	//e的后面必须跟无符号整形
        }
        scanspace(s);
        return s[i]=='\0' && flag;
    }
```

