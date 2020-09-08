### leetcode [剑指 Offer 62. 圆圈中最后剩下的数字](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)

```cpp
/*
	解法:
	1.用链表进行模拟。
	2.利用约瑟夫环的结论。
	注意:原数据的范围为从[0,n-1],每隔m-1个数移除一个数，如果到头了，则循环到开始位置。
*/
```



![剑指offer62](picture\剑指offer62.png)

```cpp
int lastRemaining(int n, int m) {
        if(n==1)    return 0;
        int last=0;
        for(int i=2;i<=n;i++)
        {
            last=(last+m)%i;
        }
        return last;
    }
```

