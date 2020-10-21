### leetcode [925. 长按键入](https://leetcode-cn.com/problems/long-pressed-name/)

> 你的朋友正在使用键盘输入他的名字 name。偶尔，在键入字符 c 时，按键可能会被长按，而字符可能被输入 1 次或多次。
>
> 你将会检查键盘输入的字符 typed。如果它对应的可能是你的朋友的名字（其中一些字符可能被长按），那么就返回 True。
>

```cpp
/*
	解法：双指针。
	时间复杂度O(min(N,M)),空间复杂度O(1)。
*/
bool isLongPressedName(string name, string typed) 
{
    int i=0,j=0;
    int N=name.size(),M=typed.size();
    int prei=i,prej=j;
    while(true)
    {
        while(i<N && name[i]==name[prei])  i++;
        while(j<M && typed[j]==typed[prej]) j++;
        if(name[prei]!=typed[prej] || (j-prej)<(i-prei))
            return false;
        if(i==N || j==M)    break;
        prei=i,prej=j;
    }
    return i==N && j==M;
}
```

