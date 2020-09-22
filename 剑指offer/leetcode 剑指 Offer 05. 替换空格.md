### leetcode [剑指 Offer 05. 替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

```cpp
/*
	解法：先统计空格的数量，然后重新计算分配的内存，之后将原来的数据逆序拷贝到新数组的位置。
*/
```

```cpp
class Solution {
public:
	void replaceSpace(char *str,int length) {
        int numofblank=0;
        for(int i=0;i<length;i++)
        {
            if(str[i]==' ')    numofblank++;
        }
        int newlength=length+2*numofblank;
        int j=newlength;
        for(int i=length;i>=0;i--)
        {
            if(str[i]!=' ')    str[j--]=str[i];
            else{
                str[j--]='0';
                str[j--]='2';
                str[j--]='%';
            }
        }
	}
};
```

