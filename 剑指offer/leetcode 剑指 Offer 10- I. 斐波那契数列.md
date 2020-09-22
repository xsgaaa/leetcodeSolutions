### leetcode [剑指 Offer 10- I. 斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

```cpp
/*
	解法:动态规划入门题，不必介绍。
*/
```

```cpp
class Solution {
public:
    int Fibonacci(int n) {
        int fib[40];
        fib[0]=0;
        fib[1]=1;
        for(int i=2;i<=n;i++)
            fib[i]=fib[i-1]+fib[i-2];
        return fib[n];
    }
};
```

