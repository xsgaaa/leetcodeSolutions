### leetcode [483. 最小好进制](https://leetcode-cn.com/problems/smallest-good-base/)

```cpp
/*
	解法：数学。
*/
```

参考：https://leetcode-cn.com/problems/smallest-good-base/solution/shu-xue-fang-fa-fen-xi-dai-ma-by-zerotrac/

核心公式：
$$
k^s<n<(k+1)^s
$$

```cpp
typedef long long ll;
    string smallestGoodBase(string n) {
        ll num=stol(n);		//将string->long long
        ll ans=num-1;		//转换成二进制形式(11)，所需的进制
        for(int i=59;i>=2;i--)
        {//逆序遍历,位数越大，最后的进制越小
            int k=pow(num,1.0/i);	//得到进制的整数部分
            if(k>1)
            {
                ll sum=1,mul=1;//计算(i+1)位的k进制表示之后的值
                for(int j=1;j<=i;j++)
                {
                    mul *=k;
                    sum+=mul;
                }
                if(sum==num)	//等于结果，则记录并退出
                {
                    ans=k;
                    break;
                }
            }
        }
        return to_string(ans);
    }
```

