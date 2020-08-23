### leetcode [201. 数字范围按位与](https://leetcode-cn.com/problems/bitwise-and-of-numbers-range/)

```
解法：当m与n位数相同时，当m等于n时说明左边相同，右边变了，再将左边移位即可。当m的位数远小于n时，中间一定存在(10000.....)这种二进制形式，最后的结果必定为0。则m当为0，表明n的位数较大，终止循环，返回0即可。
```

```cpp
int rangeBitwiseAnd(int m, int n) {
        int step=0;
        for(;m!=n && m;step++)
        {
            m=m>>1;
            n=n>>1;
        }
        return m==0?0:n<<step;
    }
```

