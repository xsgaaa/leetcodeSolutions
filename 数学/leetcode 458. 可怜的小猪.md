### leetcode [458. 可怜的小猪](https://leetcode-cn.com/problems/poor-pigs/)

```cpp
/*
	解法:数学。
	参考：https://leetcode-cn.com/problems/poor-pigs/solution/hua-jie-suan-fa-458-ke-lian-de-xiao-zhu-by-guanpen/
*/
```

```cpp
int poorPigs(int buckets, int minutesToDie, int minutesToTest) {
        //每个小猪可以涵盖states种状态
        int states = minutesToTest / minutesToDie + 1;
        //求以states为底,log(buckets)的值，然后再进行向上取整
        return ceil(log(buckets) / log(states));
        //states^(x)>=buckets，求x的值。
    }
```

